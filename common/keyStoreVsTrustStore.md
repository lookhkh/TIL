# What is KeyStore

 KeyStore란, TLS/SSL 사용 시 자신을 인증하기 위하여 자신의 인증정보, 예를 들어, 개인키, 혹은 공개키를 포함한 인증서와 같은 인증 정보를 포함한 저장소를
 나타낸다. 이때, KeyStore는 별칭(Alias)로 각각의 정보를 저장하며, SSL/TLS 상에서 자신을 인증하거나, 데이터를 암호화할 경우, 
 해당 KeyStore에서 인증정보를 가져와 사용하게 된다. 

 주요 사용처는, HTTPS 상에서 서버가 자신을 클라이언트에게 인증하기 위하여 사용되며, 몇몇의 경우, 클라이언트가 자신을 인증하기 위하여 서버에 제출하기 위하여
 사용되기도 한다.

 # TrustStore

  TrustStore란, 어플리케이션이 신뢰할 수 있는 인증서 정보를 저장하는 장소이다. 예를 들어, 웹 클라이언트가 웹 서버와 TLS Handshake를 진행하는 중, 서버는 자신의
  Certificate을 전송한다. 이때 해당 Certificate 혹은 CA가 TrustStore에 존재하지 않을 경우, TLS Handshake는 실패하게 된다.

  (https://yasarayasawardhana.medium.com/beginners-guide-to-key-stores-and-trust-stores-f7fa6d70ca2e)
