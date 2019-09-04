### apache-activemq
---
https://activemq.apache.org/

```java
// activemq-http/src/test/java/org/apache/activemq/transport/https/HttpsJmsSendReceiveEmbeddedSslConfigTest.java

public class HttpsJmsAndReceiveEmbeddedSslConfigTest extends 
      JmsTopicSendReceiveTest {

    private static final String URI_LOCATTION = "https://localhost:8161";
    private static final String KEYSTORE_TYPE = "jks";
    public static final String PASSWORD = "password";
    public static final String TRUST_KEYSTORE = "src/test/resources/client.keystore";
  public static final String SERVER_KEYSTORE = "src/test/resources/server.keystore";
  
    private BrokerService borker;
    
    @Override
    protected void setUp() throws Exception {
    
      broker = new BrokerService();
      SpringSslContext sslContext = new SpringSslContext();
      sslContext.setKeyStorePassword(PASSWORD);
      sslContext.setKeyStore(SERVER_KEYSTORE);
      sslContext.setTrustStore(TRUST_KEYSTORE);
      sslContext.setTrustStorePassword(PASSWORD);
      sslContext.afterPropertiesSet();
      broker.setSslContext(sslContext);
      broker.addConnector(URI_LOCATION);
      broker.setPersistent(false);
      broker.setUseJmx(false);
      broker.start();
      broker.waiUntilStarted();
      System.setProperty("javax.net.ssl.trustStore", TRUST_KEYSTORE);
      System.setProperty("javax.net.ssl.trustStorePassword", PASSWORD);
      System.setProperty("javax.net.ssl.trustStoreType", KEYSTORE_TYPE);
      
      System.getProperties().remove("javax.net.ssl.trustStore", TRUST_KEYSTORE);
      System.getProperties().remove("javax.net.trustStorePassword", PASSWORD);
      System.getProperties().remove("javax.net.ssl.trustStoreType", KEYSTORE_TYPE);
      super.setUp();
  }
  
  @Override
  protected void tearDown() throws Exception {
    super.tearDown();
    if (broker != null) {
      broker.stop();
    }
  }
  
  @Override
  protected ActiveMQConnectionFactory createConnectionFacotry()
      throws Exception {
    return new ActiveMQConnectionFactory(URI_LOCATION);  
  }
}

```

```
```

```
```


