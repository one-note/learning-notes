## RABIT MQ
* https://www.architect.io/blog/rabbitmq-docker-tutorial
* https://www.section.io/engineering-education/dockerize-a-rabbitmq-instance/
* https://jstobigdata.com/rabbitmq/topic-exchange-in-amqp-rabbitmq/


## Elastic serach:
* `index has unlimited documents,
index is part of one or more shard, 
shard is part of a node,
shard can be replicated across different nodes
shard is scalable`
* https://cloud.netapp.com/blog/cvo-blg-elasticsearch-architecture-7-key-components
* https://buildingvts.com/elasticsearch-architectural-overview-a35d3910e515
* https://qbox.io/blog/optimizing-elasticsearch-how-many-shards-per-index
* https://logz.io/blog/10-elasticsearch-concepts/
* https://www.elastic.co/guide/en/elasticsearch/reference/current/size-your-shards.html
* https://www.elastic.co/guide/en/elasticsearch/reference/current/cat-shards.html
* https://www.elastic.co/blog/how-many-shards-should-i-have-in-my-elasticsearch-cluster

## Cassandra:
* https://www.instaclustr.com/cassandra-architecture/
* https://www.simplilearn.com/tutorials/big-data-tutorial/cassandra-architecture#architecture_requirements_of_cassandra
* https://cassandra.apache.org/doc/latest/cassandra/architecture/guarantees.html

## Angular Links
https://www.c-sharpcorner.com/article/learn-angular-8-step-by-step-in-10-days-day-1/

https://www.tektutorialshub.com/angular-tutorial/

https://www.freecodecamp.org/news/angular-8-tutorial-in-easy-steps/


https://ultimatecourses.com/blog/category/angular/3/

https://blog.angular-university.io/

https://angular.io/docs

## CustomBeanPostProcessor

```java
package com.spring.apiversioning;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.config.BeanPostProcessor;
import org.springframework.context.ApplicationContext;
import org.springframework.stereotype.Component;

@Component
public class CustomBeanPostProcessor implements BeanPostProcessor {

    @Autowired
    private ApplicationContext applicationContext;
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {

//        if (bean instanceof RequestMappingHandlerMapping) {
//            RequestMappingHandlerMapping customized = new RequestMappingHandlerMapping() {
//
//                @Override
//                protected RequestCondition<?> getCustomMethodCondition(
//                        Method method) {
//
//                    return null;
//                }
//
//                @Override
//                protected RequestCondition<?> getCustomTypeCondition(
//                        Class<?> handlerType) {
//                    return null;
//                }
//
//            };
//            customized.setApplicationContext(((RequestMappingHandlerMapping) bean)
//                    .getApplicationContext());
//            return customized;
//        }
//        return bean;

        if(beanName.equals("requestMappingHandlerMapping"))
        {
            bean = applicationContext.getBean(ApiVersionedHandlerMapping.class);
        }
        return bean;
    }


}

```

## CustomBeanFactoryPostProcessor

```java
package com.spring.apiversioning;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.config.BeanDefinition;
import org.springframework.beans.factory.config.BeanFactoryPostProcessor;
import org.springframework.beans.factory.config.BeanPostProcessor;
import org.springframework.beans.factory.config.ConfigurableListableBeanFactory;
import org.springframework.beans.factory.support.BeanDefinitionRegistry;
import org.springframework.context.ApplicationContext;
import org.springframework.stereotype.Component;

@Component
public class CustomBeanFactoryPostProcessor implements BeanFactoryPostProcessor {

    @Override
    public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException {

        String beanRemove = "requestMappingHandlerMapping";

        BeanDefinitionRegistry registry = (BeanDefinitionRegistry) beanFactory;

        for (String beanDefinitionName : registry.getBeanDefinitionNames()) {
            BeanDefinition beanDefinition = registry.containsBeanDefinition(beanRemove) ? registry.getBeanDefinition(beanDefinitionName) : null;
            if (beanDefinition != null ) {

                if (registry.containsBeanDefinition(beanRemove)) {

                    registry.removeBeanDefinition(beanRemove);
                }
            }
        }
    }
}

```

## ReuestMappingHandlerMapping (requestMapping place holder resolution)
```java
package com.spring.apiversioning;

import org.springframework.context.annotation.Primary;
import org.springframework.core.annotation.Order;
import org.springframework.http.MediaType;
import org.springframework.lang.Nullable;
import org.springframework.stereotype.Component;
import org.springframework.util.Assert;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.mvc.condition.*;
import org.springframework.web.servlet.mvc.method.RequestMappingInfo;
import org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping;

import java.lang.annotation.Annotation;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;
import java.util.Arrays;
import java.util.Map;
import java.util.Set;

@Component
@Primary
public class ApiVersionedHandlerMapping extends RequestMappingHandlerMapping {

//    @Override
    protected void registerHandlerMethod1(Object handler, Method method, RequestMappingInfo mapping) {
        ProducesRequestCondition condition = mapping.getProducesCondition();
        Set<MediaTypeExpression> mediaTypeExpressionSet = condition.getExpressions();
        MediaTypeExpression tempMediaType = null;
        for (MediaTypeExpression mediaTypeExpression : mediaTypeExpressionSet) {
            if (mediaTypeExpression.getMediaType().toString().equals("application/version")) {
                tempMediaType = mediaTypeExpression;
                break;
            }
        }
        String[] arr = null;
        //{"application/vnd.company.app-v1+json"};
        if (mediaTypeExpressionSet.remove(tempMediaType)) {
            String packageName = null; // get pkg name from method
            arr = new String[]{"application/vnd.company.app-v1+json"};
            mediaTypeExpressionSet.addAll(new ProducesRequestCondition(arr).getExpressions());
            condition.combine(new ProducesRequestCondition(arr));
        }

        RequestMappingInfo requestMappingInfo = new RequestMappingInfo(
                "n1",
                mapping.getPatternsCondition(),
                mapping.getMethodsCondition(),
                mapping.getParamsCondition(),
                mapping.getHeadersCondition(),
                mapping.getConsumesCondition(),
                arr==null ? mapping.getProducesCondition(): new ProducesRequestCondition(arr),
                mapping.getCustomCondition()
        );
      //  super.registerHandlerMethod(handler, method, requestMappingInfo);
    }

//    @Override
    public void registerMapping1(RequestMappingInfo mapping, Object handler, Method method) {
        ProducesRequestCondition condition = mapping.getProducesCondition();
        Set<MediaTypeExpression> mediaTypeExpressionSet = condition.getExpressions();
        MediaTypeExpression tempMediaType = null;
        for (MediaTypeExpression mediaTypeExpression : mediaTypeExpressionSet) {
            if (mediaTypeExpression.getMediaType().toString().equals("application/version")) {
                tempMediaType = mediaTypeExpression;
                break;
            }
        }
        if (mediaTypeExpressionSet.remove(tempMediaType)) {
            String packageName = null; // get pkg name from method
            String[] arr = {"application/vnd.company.app-v1+json"};
            mediaTypeExpressionSet.addAll(new ProducesRequestCondition(arr).getExpressions());
        }
       // super.registerMapping(mapping, handler, method);
    }

    @Override
    protected RequestMappingInfo createRequestMappingInfo(RequestMapping requestMapping, RequestCondition<?> customCondition) {


        RequestMapping newAnnotation = new RequestMapping() {

            @Override
            public String name() {
                return requestMapping.name();
            }

            @Override
            public String[] value() {
                return requestMapping.value();
            }

            @Override
            public String[] path() {
                return requestMapping.path();
            }

            @Override
            public RequestMethod[] method() {
                return requestMapping.method();
            }

            @Override
            public String[] params() {
                return requestMapping.params();
            }

            @Override
            public String[] headers() {
                return requestMapping.headers();
            }

            @Override
            public String[] consumes() {
                return requestMapping.consumes();
            }

            @Override
            public String[] produces() {

                String[] produces = requestMapping.produces();
                VersionUtils.replaceVersioningPlaceHolders(produces);
                return produces;
            }

            @Override
            public Class<? extends Annotation> annotationType() {
                return requestMapping.annotationType();
            }
        };

        return super.createRequestMappingInfo(newAnnotation, customCondition);
    }

    @Override
    public int getOrder() {
        return -1;
    }

}
```

https://stackoverflow.com/questions/2811769/adding-an-http-header-to-the-request-in-a-servlet-filter

https://howtodoinjava.com/java/servlets/httpservletrequestwrapper-example-read-request-body/
