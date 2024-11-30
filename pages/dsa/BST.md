<div align='center'>

# Binary Search Tree (BST)

</div>

<br><br>

#### Insert, Display by In-Order and Searching

```php
class Node 
{
    public $value;
    public $left;
    public $right;

    public function __construct($value) 
    {
        $this->value = $value;
        $this->left = null;
        $this->right = null;
    }
}

class BST 
{
    public $root;

    public function __construct() 
    {
        $this->root = null;
    }

    public function insert($value) 
    {
        $this->root = $this->insertRec($this->root, $value);

        echo "Inserted value: $value\n"; // Print confirmation message
    }

    private function insertRec($node, $value) 
    {
        if ($node == null) {
            return new Node($value);
        }

        if ($value < $node->value) {
            $node->left = $this->insertRec($node->left, $value);
        } else {
            $node->right = $this->insertRec($node->right, $value);
        }
        return $node;
    }

    public function inOrderTraversal($node) 
    {
        if ($node != null) {
            $this->inOrderTraversal($node->left);
            echo $node->value . " "; // Print node value
            $this->inOrderTraversal($node->right);
        }
    }

    public function search($node, $value) 
    {
        // Base case: If node is null or value is found
        if ($node == null) {
            return false; // Value not found
        }
    
        if ($node->value == $value) {
            return true; // Value found
        }
    
        // Recursive case: Search left or right subtree
        if ($value < $node->value) {
            return $this->search($node->left, $value); // Search in left subtree
        } else {
            return $this->search($node->right, $value); // Search in right subtree
        }
    }
}

// Usage
$bst = new BST();
$bst->insert(10);
$bst->insert(5);
$bst->insert(15);
$bst->insert(7);
$bst->insert(3);

echo "\n";
// Visualize tree using in-order traversal
echo "In-Order Traversal: ";
$bst->inOrderTraversal($bst->root);
echo "\n\n";


// Search for values
$searchValue = 7;
$result = $bst->search($bst->root, $searchValue);
if ($result) {
    echo "Value $searchValue found in the BST.\n";
} else {
    echo "Value $searchValue not found in the BST.\n";
}
```


Output :

```bash
// Insert
Inserted value: 10
Inserted value: 5
Inserted value: 15
Inserted value: 7
Inserted value: 3

// Display Assending Order
In-Order Traversal: 3 5 7 10 15 

// Search let = 7
Value 7 found in the BST.
```