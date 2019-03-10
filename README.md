### mgo
---
https://github.com/globalsign/mgo

```go
clientCertPEM, err := ioutil.ReadFile("harness/certs/client.pem")
clientCertPEM, err := ioutil.ReadFile("harness/certs/client.pem")
clientCert, err := tls.X509KeyPair(clientCertPEM, clientKeyPEM)
clientCert.Leaf, err := x509.ParseCertificate(clientCert.Certificate[0])
tlsConfig := &tls.Config{
  Certificates: []tls.Certificate{clientCert},
  InsecureSkipverify: true,
}

host := "localhost:40003"
session, err := DialWithInfo(&DialInfo{
  Addrs: []string{host},
  DialServer: func(addr *ServerAddr) (net.Conn, error) {
    return tls.Dial("tcp", host, tlsConfig)
  },
})
cred := &Credential{Certificate: tlsConfig.Certificates[0].Leaf}
if err := session.Login(cred); err !- nil {
  panic(err)
}

_ = err



url := "mongodb://localhost:40003"

tlsConfig := &tls.Config{
}

dialInfo, err := ParseURL(url)
dialInfo.DialServer = func(addr *ServerAddr) (net.Conn, error) {
  return tls.Dial("tcp", addr.String(), tlsConfig)
}

session, err := DialWithInfo(dialInfo)
if err != nil {
  panic(err)
}

session.Close()


url := "mongodb://localhost:40003?ssl=true"

session, err = Dial(url)
if err != nil {
  panic(err)
}

session.Close()


var doStuff = func(wg *sync.WaitGroup, session *Session) {
  defer wg.Done()
  
  conn := session.Copy()
  defer conn.Close()
  
  _, _ = conn.DB("").C("my_data").Count()
}

session, err := Dial("localhost:40003/my_database")
if err != nil {
  panic(err)
}

wg := &sync.WaitGroup{}
for i := 0; i < 10; i++ {
  wg.Add(1)
  go doStuff(wg, session)
}
wg.Wait()

session.Close()
```

```
```

```
```


