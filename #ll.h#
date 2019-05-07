#ifndef _LL_H_
#define _LL_H_
#include <assert.h>

#include <cstdlib>
#include <exception>
#include <stdexcept>

//YOUR CODE GOES HERE

template<typename T>
class LinkedList
{
  class Node
  {
   public:
    T data;
    Node * next;
    Node * prev;

    Node(const T & d) : data(d), next(NULL), prev(NULL) {}  // default contructor for node
    Node(const T & d, Node * n, Node * p) :
        data(d),
        next(n),
        prev(p) {}  // non trivial constructor for node
  };
  Node * head;
  Node * tail;
  int size;

 public:
  LinkedList() : head(NULL), tail(NULL), size(0) {}  // default constructor
  LinkedList(const LinkedList<T> & rhs) : head(NULL), tail(NULL), size(rhs.size) {
    Node * current_rhs = rhs.head;
    Node * current_lhs = NULL;

    for (int i = 0; i < rhs.size; i++) {
      if (head == NULL) {
        head = new Node(current_rhs->data, NULL, NULL);
        current_lhs = head;
        current_rhs = current_rhs->next;
      }
      else {
        current_lhs->next = new Node(current_rhs->data, NULL, NULL);
        current_lhs->next->prev = current_lhs;
        current_lhs = current_lhs->next;
        current_rhs = current_rhs->next;
      }
      tail = current_lhs;
    }
  }  // copy constructor

  LinkedList<T> & operator=(const LinkedList<T> & rhs) {
    if (this != &rhs) {
      Node * temp_rhs = rhs.head;  // pointer to iterate through rhs LL
      Node * temp_new = NULL;      // pointer to front of new LL.
      Node * curr = NULL;          // pointer to iterate through new LL.

      while (temp_rhs != NULL) {
        if (temp_new == NULL) {
          temp_new = new Node(temp_rhs->data, NULL, NULL);
          curr = temp_new;
          temp_rhs = temp_rhs->next;
        }
        else {
          curr->next = new Node(temp_rhs->data, NULL, NULL);
          curr->next->prev = curr;
          curr = curr->next;
          temp_rhs = temp_rhs->next;
        }
      }  // create the new LL

      while (head != NULL) {
        Node * temp_del = head->next;
        delete head;
        head = temp_del;
      }  // delete the original LL.

      head = temp_new;
      tail = curr;
      size = rhs.size;
    }
    return *this;
  }  // assignment operator.

  ~LinkedList() {
    while (head != NULL) {
      Node * temp = head->next;
      delete head;
      head = temp;
    }
  }  // destructor

  void addFront(const T & item) {
    head = new Node(item, head, NULL);
    if (tail == NULL) {
      tail = head;
    }
    else {
      head->next->prev = head;
    }
    size++;
  }  // addfront method

  void addBack(const T & item) {
    tail = new Node(item, NULL, tail);
    if (head == NULL) {
      head = tail;
    }
    else {
      tail->prev->next = tail;
    }
    size++;
  }  // add back method

  bool remove(const T & data) {
    Node * curr = head;  // assign pointer to iterate through list.
    int var_remove = 0;
    while (curr != NULL) {
      if (curr->data == data && curr->prev == NULL && curr->next == NULL) {
        delete curr;  // case #1: one node list.
        size--;
        head = NULL;  // see if you need to assign this to NULL.
        var_remove = 1;
        break;
      }
      else if (curr->data == data) {
        Node * temp1 = curr->prev;
        Node * temp2 = curr->next;
        if (temp1 == NULL) {
          delete curr;
          size--;
          var_remove = 1;
          temp2->prev = NULL;
          head = temp2;
          break;
        }
        else if (temp2 == NULL) {
          delete curr;
          size--;
          var_remove = 1;
          temp1->next = NULL;
          tail = temp1;
          break;
        }
        else {
          delete curr;
          size--;
          var_remove = 1;
          temp1->next = temp2;
          temp2->prev = temp1;
          break;
        }
      }
      curr = curr->next;
    }

    if (var_remove == 1) {
      return true;
    }
    else {
      return false;
    }  // remove method
  }
  T & operator[](int index) const {
    Node * temp = head;

    for (int i = 0; i < index; i++) {
      if (index >= size) {
        throw(std::out_of_range("Index out of range"));
      }
      else {
        temp = temp->next;
      }
    }
    return temp->data;
  }  // [] operator const.

  T & operator[](int index) {
    Node * temp = head;

    for (int i = 0; i < index; i++) {
      if (index >= size) {
        throw(std::out_of_range("Index out of range"));
      }
      else {
        temp = temp->next;
      }
    }
    return temp->data;

  }  // [] operator nonconst

  int find(const T & item) const {
    int counter = 0;
    int exist = 0;
    Node * temp = head;  // pointer to iterate through list
    while (temp != NULL) {
      if (temp->data == item) {
        exist = 1;
        break;
      }
      else {
        temp = temp->next;
        counter++;
      }
    }
    if (exist == 1) {
      return counter;
    }
    else {
      return -1;
    }
  }  // find method

  int getSize() const { return size; }  // getSize method
};

#endif
