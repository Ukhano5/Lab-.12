# Lab-.12
Muhammad Umair
12370
SE 3rdC

 Q1: Implement a function to search for a word in a trie.
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True

    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word

Output for Q1: No direct output, as it is a set of class and method definitions.

Q2: Write a function to find all words in a trie that start with a given prefix.
class TrieNodeWithPrefixCount(TrieNode):
    def __init__(self):
        super().__init__()
        self.prefix_count = 0

class TrieWithPrefixCount(Trie):
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNodeWithPrefixCount()
            node.prefix_count += 1
            node = node.children[char]
        node.is_end_of_word = True
        node.prefix_count += 1

    def words_with_prefix(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return []
            node = node.children[char]
        return self._find_words_from_node(node, prefix)

    def _find_words_from_node(self, node, current_word):
        result = []
        if node.is_end_of_word:
            result.append(current_word)
        for char, child_node in node.children.items():
            result.extend(self._find_words_from_node(child_node, current_word + char))
        return result

Output for Q2: No direct output, as it is a set of class and method definitions.

 Q3: Solve a real-world problem using a tree data structure:
# Problem: Managing Book Inventory
# Design: Use a tree structure to represent book categories and subcategories, where each node represents a category.
#         Books are stored at the leaf nodes, and each node keeps track of the total number of books in that category.
#         This allows efficient categorization, search, and retrieval of books in a bookstore's inventory.

class BookNode:
    def __init__(self):
        self.books = {}  # Book details (e.g., title, author, quantity)
        self.children = {}

class BookInventoryTree:
    def __init__(self):
        self.root = BookNode()

    def add_book(self, category, book_details):
        node = self.root
        for category_part in category:
            if category_part not in node.children:
                node.children[category_part] = BookNode()
            node = node.children[category_part]
        book_title = book_details['title']
        if book_title not in node.books:
            node.books[book_title] = book_details
        else:
            node.books[book_title]['quantity'] += book_details['quantity']

    def find_books_in_category(self, category):
        node = self.root
        for category_part in category:
            if category_part not in node.children:
                return []
            node = node.children[category_part]
        return list(node.books.values())

Output  No direct output, as it is a set of class and method definitions.
