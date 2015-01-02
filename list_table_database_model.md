# List Table Database Model

If your model is a database table you can use the `WPDKDBListTableModel` class. This class is an extends of `WPDKListTableModel`. In practice `WPDKDBListTableModel` is a merge of `WPDKDBTableModel` and `WPDKListTableModel`.

---

> **NOTE WELL** PHP does not allow to inherit from more than one class. So one way to solve the problem is to provide a pointer to the class that you want to inherit. This class, therefore, is as if it were understood in this way: `class WPDKDBListTableModel extends WPDKListTableModel, WPDKDBTableModel {}`

---
                                                                                
### Typical scheme

Usually you'll have

1. Single class item
2. Model data class
3. List table view controller
4. Single new/edit view

For example, if you have manage a books you'll have

1. Class `Book` - file `book.php`
2. Class `BooksModel` - file `books-model.php`
3. Class `BooksListTableViewController` - file `books-listtable-viewcontroller.php`
4. Class `BookEditView` - file `book-edit-view.php`