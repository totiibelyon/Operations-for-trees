# #include <stdio.h>
#include <stdlib.h>

// i & iv. Creating a node using structure pointers
struct Node {
    char data;
    struct Node* left;  // Pointer to left child
    struct Node* right; // Pointer to right child
};

// Helper function to dynamically allocate a new node
struct Node* createNode(char data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        printf("Out of memory!\n");
        exit(1);
    }
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// ii. Functions - Pre-order Traversal (Root, Left, Right)
void preOrder(struct Node* root) {
    if (root == NULL) return;
    printf("%c ", root->data);
    preOrder(root->left);
    preOrder(root->right);
}

// ii. Functions - In-order Traversal (Left, Root, Right)
void inOrder(struct Node* root) {
    if (root == NULL) return;
    inOrder(root->left);
    printf("%c ", root->data);
    inOrder(root->right);
}

// ii. Functions - Post-order Traversal (Left, Right, Root)
void postOrder(struct Node* root) {
    if (root == NULL) return;
    postOrder(root->left);
    postOrder(root->right);
    printf("%c ", root->data);
}

// ii. Functions - Level-order Traversal (Using a simple array-based queue)
void levelOrder(struct Node* root) {
    if (root == NULL) return;

    // Creating an array queue to hold node pointers
    struct Node* queue[100];
    int front = 0;
    int rear = 0;

    // Enqueue root
    queue[rear++] = root;

    while (front < rear) {
        // Dequeue current element
        struct Node* current = queue[front++];
        printf("%c ", current->data);

        // Enqueue left child
        if (current->left != NULL) {
            queue[rear++] = current->left;
        }
        // Enqueue right child
        if (current->right != NULL) {
            queue[rear++] = current->right;
        }
    }
}

// Clean up function to free memory allocations
void freeTree(struct Node* root) {
    if (root == NULL) return;
    freeTree(root->left);
    freeTree(root->right);
    free(root);
}

int main() {
    /*
       Building a tree to match the level order written at the top of the image: 
       Level Order -> A, B, C, D, E, F, G
             A
           /   \
          B     C
         / \   / \
        D   E F   G
    */
    struct Node* root = createNode('A');
    root->left = createNode('B');
    root->right = createNode('C');
    root->left->left = createNode('D');
    root->left->right = createNode('E');
    root->right->left = createNode('F');
    root->right->right = createNode('G');

    // iii. Call all the functions
    printf("--- Binary Tree Traversals (C Language) ---\n");

    printf("Pre-order Traversal:   ");
    preOrder(root);
    printf("\n");

    printf("In-order Traversal:    ");
    inOrder(root);
    printf("\n");

    printf("Post-order Traversal:  ");
    postOrder(root);
    printf("\n");

    printf("Level-order Traversal: ");
    levelOrder(root);
    printf("\n");

    // Clean up memory before exiting
    freeTree(root);

    return 0;
}
