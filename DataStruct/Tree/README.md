### 1 二叉树的特性
- 结点数与边数：一棵二叉树有n个元素，n > 0，则它有m = n - 1条边。
- 已知高度求结点数：一棵二叉树的高度为h，h ≥ 0，则它最少有h个元素，最多有2<sup>h</sup>-1个元素。   
   第i层最多有2<sup>i-1</sup>个结点。
- 已知结点数求高度：一棵二叉树有n个结点，n > 0，则它的最大高度为n，最小高度为log<sub>2</sub>(n+1)的上取整。
- 完全二叉树的下标：（计算机对整数会自动下取整）  
  1. 当下标是1开始时，第i个结点的父结点为i/2，左孩子为2\*i，右孩子为2\*i+1
  2. 当下标是0开始时，第i个结点的父节点为(i-1)/2，坐孩子为2\*i+1，右孩子为2\*i+2

### 2 二叉树的实现
- 数组实现  
  1. 完全二叉树适合用数组实现
  2. [数组实现的二叉树](./arrayBinaryTree.h)   
    - T searchNode(int theIndex)：根据索引（数组下标）寻找结点
    - void addNode(int theIndex, int direction, T \*pNode): 添加结点，theIndex是待插入结点的父结点的索引（数组下标），direction = 0代表左子树，direction = 1代表右子树，pNode是待插入的值
    - void deleteNode(int theIndex, T \*pNode)：删除结点，将被删除的结点放到pNode中返回
    - void treeTrave()：遍历结点  

- 链表实现  
  1. 非完全二叉树适合用链表实现
  2. [链表实现的二叉树](./linkedBinaryTree.h)  
    - bool empty()：判断树是否为空
    - int size()：树的结点数
    - T\* rootElement()：返回根结点的值
    - void makeTree(const T& element, linkedBinaryTree<T>&, linkedBinaryTree<T>&)：给定根结点、左子树和右子树，创建一块新的树
    - linkedBinaryTree<T>& removeLeftSubtree()：删除并返回左子树
    - linkedBinaryTree<T>& removeRightSubtree()：删除并返回右子树
    - void **preOrder**()：先序遍历
    - void **preOrderUnRecursive**()：先序遍历（非递归版本）
    - void **inOrder**()：中序遍历
    - void **inOrderUnRecursive**()：中序遍历（非递归版本）
    - void **postOrder**()：后续遍历
    - void **postOrderUnRecursive**()：后序遍历（非递归版本）
    - void **levelOrder**()：层次遍历
    - int **height**()：树的高度

### 3 二叉树的遍历
- 前序遍历  
  1. 递归版本：先访问根结点，再递归访问左子树、右子树。递归的终止条件是树为空。
  2. 非递归版本：对于任一结点，其可看做是根结点，因此可以直接访问，访问完之后，若其左孩子不为空，按相同规则访问它的左子树；当访问完其左子树时，再访问它的右子树。（用栈实现）
- 中序遍历  
  1. 递归版本：先递归访问左子树，再访问根结点，最后递归访问右子树。递归的终止条件是树为空。
  2. 非递归版本：对于任一结点，优先访问其左孩子，而左孩子结点又可以看做一根结点，然后继续访问其左孩子结点，直到遇到左孩子结点为空的结点才进行访问，然后访问其右子树。（用栈实现）
- 后序遍历  
  1. 递归版本：先递归访问左子树，然后递归访问右子树，最后访问根结点。递归的终止条件是树为空。
  2. 非递归版本：对于任一结点P，如果P不存在左孩子和右孩子，则可以直接访问它；或者P存在左孩子或者右孩子，但是其左孩子和右孩子都已被访问过了，则同样可以直接访问该结点。（用栈实现）
- 层次遍历  
  层次遍历是一层一层访问树的结点，可以用队列来实现
- 前序遍历、中序遍历和后序遍历的非递归实现对比
  1. 三者相同的都是在p指针为空且栈为空是退出循环。
  2. 外圈while循环内前一步不断寻找到最左的孩子的方法基本相同。
  3. 不同的主要在p指针为空需要出栈后的操作：
    - 先序遍历是在前面寻找最左孩子时就已经visit结点，后面出栈后是直接让指针p指向出栈结点的右孩子；
    - 中序遍历在后面出栈时，先visit出栈的结点，再让指针p指向出栈的结点的右孩子；
    - 后序遍历多了个pre指针指向前一个visit过的结点；出栈前需要检查确保栈顶结点的右孩子为空或者被visit过 才能出栈visit该出栈的结点，如果栈顶结点的右孩子不为空且还没被visit过 就不出栈 让p指针p指向栈顶元素的右孩子。

### 4 二叉树的应用
 - [并查集](../../Algorithms/search/unionFind.h)

