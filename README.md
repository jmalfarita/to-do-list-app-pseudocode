# to-do-list-app-pseudocode

START 
IMPORT tkinter as tk 
IMPORT messagebox from tkinter 
CLASS TodoApp: 
    FUNCTION __init__(self, root): 
        SET self.root = root 
        SET title of self.root to "To-Do List App (Stack/Queue)" 
        SET geometry of self.root to "400x500" 
        SET self.mode = tk.StringVar with initial value "Stack" 
        SET self.tasks = an empty list 
        CREATE a Label with text "To-Do List App", font ("Arial", 18, "bold"), and pack with 
pady=10 
        CREATE a Label with text "Mode:" and pack 
        CREATE an OptionMenu with self.root, self.mode, options "Stack", "Queue", and pack 
        CREATE an Entry widget with width 30, set to self.entry, and pack with pady=10 
        CREATE a Button with text "Add Task", command self.add_task, and pack with pady=5 
        CREATE a Button with text "Remove Task", command self.remove_task, and pack with 
pady=5 
        CREATE a Button with text "Clear All", command self.clear_tasks, and pack with pady=5 
        CREATE a Listbox widget with width 45, height 10, set to self.task_display, and pack with 
pady=10 
        CREATE a Label with text "Mode: Stack (LIFO)", foreground "gray", set to self.status, and 
pack with pady=5 
        CREATE a Button with text "Exit", foreground "white", background "red", command 
self.confirm_exit, and pack with pady=10 
        CALL self.mode.trace_add("write", self.update_mode) 
    FUNCTION add_task(self): 
        SET task = get text from self.entry, remove leading/trailing whitespace 
        IF task is not empty THEN 
            APPEND task to self.tasks 
            CALL self.update_display() 
            DELETE all text in self.entry 
ELSE 
            DISPLAY a warning message box with title "Input Error" and message "Please enter a 
task." 
        END IF 
    FUNCTION remove_task(self): 
        IF self.tasks is not empty THEN 
            IF self.mode.get() is "Stack" THEN 
                SET removed = remove and return the last element from self.tasks 
            ELSE IF self.mode.get() is "Queue" THEN 
                SET removed = remove and return the first element from self.tasks 
            END IF 
            CALL self.update_display() 
            DISPLAY an information message box with title "Task Removed" and message 
"Removed: {removed}" 
        ELSE 
            DISPLAY an information message box with title "No Tasks" and message "There are no 
tasks to remove." 
        END IF 
    FUNCTION clear_tasks(self): 
        CLEAR all elements from self.tasks 
        CALL self.update_display() 
    FUNCTION update_display(self): 
        DELETE all items in self.task_display 
        FOR each index and task in self.tasks: 
            INSERT into self.task_display the string "{index+1}. {task}" at the end 
        END FOR 
    FUNCTION update_mode(self, *args): 
        SET mode = get value of self.mode 
        IF mode is "Stack" THEN 
            SET text of self.status to "Mode: Stack (LIFO)" 
        ELSE IF mode is "Queue" THEN 
            SET text of self.status to "Mode: Queue (FIFO)" 
        END IF 
    FUNCTION confirm_exit(self): 
        SET answer = DISPLAY a yes/no question message box with title "Exit Confirmation" and 
message "Are you sure you want to exit?" 
        IF answer is true THEN 
            DESTROY self.root 
        END IF
END CLASS 
IF __name__ == "__main__": 
    CREATE a main window, root = tk.Tk() 
    CREATE an instance of TodoApp, app = TodoApp(root) 
    START the Tkinter event loop, root.mainloop() 
END     
