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
  Socket(Protocollo protcol, Address* address = null);
  
  public:
  void broadcastOn();
  ⁓Socket();
}

class SocketUDP:public Socket{
  
  public:
  SocketUDP(Address* address = null);
  bool sendUDPmsg(char* content, Address reciver);
  char* recvUDPmsg(Address* emitter);
  ⁓SocketUDP();
}

//TCP use below calsses [RFN]

class Node;
class Lista;
class Connection;
class ClientConn;
class ServerConn;

class SocketTCP:public Socket{
  
  protected:
  SocketTCP(Address* address = null);
  ⁓SocketTCP();
}

class ClientTCP:public SocketTCP{
  
  private: 
  ClientConn* channel;
  
  public:
  ClientTCP();
  void connect(Address server);
  bool sendTCPmsg(char* content);
  char* recvTCPmsg();
  ⁓ClientTCP();
}

class ServerTCP:public SocketTCP{
  
  private: 
  Lista* ConnList;
  
  public:
  ServerTCP(Address address);
  ServerConn* accept();
  ⁓ServerTCP();
}

class Node{
  
  private:
  Node* nextNode;
  
  public:
  Node();
  Node* getNext();
  virtual void getKey() = 0;
  ⁓Node();
}

class Lista{
  private:
  Node* first;
  void deleteAll(Node* toDelete);
  void show(Node* toShow);
  
  public:
  Lista();
  void add(Node* toAdd);
  void show();
  ⁓Lista();
}

class Connection{
  
  private:
  Address address;
  int connID;
  
  protected:
  Connection(int connID, Address address);
  
  public:
  bool sendTCPmsg(char* content);
  char* recvTCPmsg();
  Address getAddress();
  ⁓Connection();
}

class ClientConn:public Connection{
  
  public:
  ClientConn(int sockID, Address address);
  ⁓ClientConn();
}

class ServerConn:public Connection, public Node{
  
  public:
  ServerConn(int connID, Address address);
  void* getKey();
  ⁓ServerConn();
}

#endif
