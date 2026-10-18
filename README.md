# Merge2BSTs-C-DSA
This is a c++ DSA Tree solution 

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node(int val) {
        data = val;
        left = right = NULL;
    }
};

Node* insert(Node* root, int val) {
    if (root == NULL) {
        return new Node(val);
    }

    if (val < root->data) {
        root->left = insert(root->left, val);
    } else {
        root->right = insert(root->right, val);
    }

    return root;
}

void inorder(Node* root, vector<int>& arr) {
    if (root == NULL) {
        return;
    }

    inorder(root->left, arr);
    arr.push_back(root->data);
    inorder(root->right, arr);
}

vector<int> mergeBSTs(Node* root1, Node* root2) {
    vector<int> arr1, arr2, result;

    inorder(root1, arr1);
    inorder(root2, arr2);

    int i = 0, j = 0;

    while (i < arr1.size() && j < arr2.size()) {
        if (arr1[i] < arr2[j]) {
            result.push_back(arr1[i++]);
        } else {
            result.push_back(arr2[j++]);
        }
    }

    while (i < arr1.size()) {
        result.push_back(arr1[i++]);
    }

    while (j < arr2.size()) {
        result.push_back(arr2[j++]);
    }

    return result;
}

int main() {
    Node* root1 = NULL;
    Node* root2 = NULL;

    // First BST
    root1 = insert(root1, 0);
    root1 = insert(root1, 2);
    root1 = insert(root1, 5);

    // Second BST
    root2 = insert(root2, 1);
    root2 = insert(root2, 3);
    root2 = insert(root2, 8);
    root2 = insert(root2, 10);

    vector<int> result = mergeBSTs(root1, root2);

    cout << "Merged BST values: ";

    for (int val : result) {
        cout << val << " ";
    }

    cout << endl;

    return 0;
}
