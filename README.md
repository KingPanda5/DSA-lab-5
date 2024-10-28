# DSA-lab-5

EXERCISE 1:

Cpp file:
#include <iostream>
using namespace std;

class Node {
public:
    int data;
    Node* prev;
    Node* next;

    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

class DList {
private:
    Node* head;

public:
    DList() : head(nullptr) {}

    // Checks if the list is empty or not
    bool emptyList() {
        return head == nullptr;
    }

    // Inserts a new node at the start of the list
    void insert_begin(int value) {
        Node* newNode = new Node(value);
        if (emptyList()) {
            head = newNode;
        }
        else {
            newNode->next = head;
            head->prev = newNode;
            head = newNode;
        }
    }

    // Inserts a new node at the end of the list
    void insert_end(int value) {
        Node* newNode = new Node(value);
        if (emptyList()) {
            head = newNode;
        }
        else {
            Node* temp = head;
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
            newNode->prev = temp;
        }
    }

    // Inserts a new node with value 'newV' after the node containing value 'oldV'
    void insert_after(int oldV, int newV) {
        Node* temp = head;
        while (temp != nullptr && temp->data != oldV) {
            temp = temp->next;
        }
        if (temp != nullptr) { // oldV found
            Node* newNode = new Node(newV);
            newNode->next = temp->next;
            newNode->prev = temp;
            if (temp->next != nullptr) {
                temp->next->prev = newNode;
            }
            temp->next = newNode;
        }
    }

    // Deletes the node containing the specified value
    void deleteNode(int value) {
        Node* temp = head;
        while (temp != nullptr && temp->data != value) {
            temp = temp->next;
        }
        if (temp == nullptr) return; // Value not found

        if (temp->prev != nullptr) {
            temp->prev->next = temp->next;
        }
        else {
            head = temp->next;
        }
        if (temp->next != nullptr) {
            temp->next->prev = temp->prev;
        }
        delete temp;
    }

    // Displays the values stored in the list starting from head
    void traverse() {
        Node* temp = head;
        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }
};

int main() {
    DList list;
    list.insert_begin(10);
    list.insert_end(20);
    list.insert_end(30);
    list.insert_after(20, 25);
    list.traverse(); // Output: 10 20 25 30

    list.deleteNode(25);
    list.traverse(); // Output: 10 20 30

    list.insert_begin(5);
    list.traverse(); // Output: 5 10 20 30

    return 0;
}

EXERCISE 2:


    // Function to reverse the doubly linked list
    void reverse() {
        Node* temp = nullptr;
        Node* current = head;

        // Swap next and prev for all nodes of the list
        while (current != nullptr) {
            temp = current->prev;
            current->prev = current->next;
            current->next = temp;
            current = current->prev;
        }

        // Adjust head to be the last element
        if (temp != nullptr) {
            head = temp->prev;
        }
    }


    // Function to display contents of alternate nodes starting from head
    void display_alternate() {
        Node* temp = head;
        bool display = true;
        while (temp != nullptr) {
            if (display) {
                cout << temp->data << " ";
            }
            display = !display;
            temp = temp->next;
        }
        cout << endl;
    }



