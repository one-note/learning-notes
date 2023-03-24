Below services can be used:
- url-service
- id generator
- base62-encoder

# URL SERVICES
- recevies an URL
- gets the id from an id-generator
- send the id to base62-encoder
- saves the URL and base62 encoded URL into database

# id-generator service
- we may have replicated id-generator service.
- each replica will serve different range of id.
  > For example pod-1 can serve id from 0-1 lakh
- it can have internal counter that increase the counter from 0 to 1 lakh
- it can persist the last id created in a cloud storage

# base62 encoder

- we are using characters as 0-9, a-z, A-Z. total 62 characters.
- here is the code for mapping
  ```java
   Map<Integer,Character> map = new HashMap<>();
    for(int i=0; i<10;i++) // 0-9
    {
      map.put(i,Character.forDigit(i,10));
    }
    for(int i=65;i<91;i++) // A-Z
    {
      map.put(i-55,(char)i);
    }
    for(int i=97;i< 123;i++) // a-z
    {
      map.put(i-60,(char)i);
    }
    map.entrySet()
        .stream().forEach(e->{
          System.out.println(e.getKey()+" "+e.getValue());
        });
  ```
  {0=0, 1=1, 2=2, 3=3, 4=4, 5=5, 6=6, 7=7, 8=8, 9=9, 10=A, 11=B, 12=C, 13=D, 14=E, 15=F, 16=G, 17=H, 18=I, 19=J, 20=K, 21=L, 22=M, 23=N, 24=O,
  25=P, 26=Q, 27=R, 28=S, 29=T, 30=U, 31=V, 32=W, 33=X, 34=Y, 35=Z, 37=a, 38=b, 39=c, 40=d, 41=e, 42=f, 43=g, 44=h, 45=i, 46=j, 47=k, 48=l, 49=m, 
  50=n, 51=o, 52=p, 53=q, 54=r, 55=s, 56=t, 57=u, 58=v, 59=w, 60=x, 61=y, 62=z}
- let say we receive an value (780)
- now if we convert this to base 62 then we will have values like: [12,18] : [C,I] : CI
  ```java
   long l = 762;
    long r = 0;
    int base = 62;
    while (l > 0) {
      r = l % base;
      l = l / base;
      System.out.println(r);
    }
  ```
- so for 780 we return CI
