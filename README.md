# Connections
Road for nowhere

// Here u can find  the Socket implementation [RFN]

#ifndef SOCK_HPP
#define SOCK_HPP

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>

#define CONNECTIONS 50
#define MSGLENGHT 4096

class Socket{
  
  protected: 
  int sockID;
  Socket(Protocollo protcol, Address* address = null){}
  
  public:
  void broadcastOn(){}
  ⁓Socket(){}
}

class SocketUDP:public Socket{
  
  public:
  SocketUDP(Address* address = null){}
  bool sendUDPmsg(char* content, Address reciver){}
  char* recvUDPmsg(Address* emitter){}
  ⁓SocketUDP(){}
}

class SocketTCP:public Socket{
  
  protected:
  SocketTCP(Address* address = null){}
  ⁓SocketTCP(){}
}

class ClientTCP:public SocketTCP{
  
  private: 
  ClientConn* channel;
  
  public:
  ClientTCP(){}
  void connect(Address server);
  bool sendTCPmsg(char* content);
  char* recvTCPmsg();
  ⁓ClientTCP(){}
}

class ServerTCP:public SocketTCP{
  
  private: 
  Lista* ConnList;
  
  public:
  ClientTCP(){}
  void connect(Address server);
  bool sendTCPmsg(char* content);
  char* recvTCPmsg();
  ⁓ClientTCP(){}
}

#endif
