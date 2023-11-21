import tkinter as tk

def autocomplete(event):
    input_text = entry.get().lower()
    input_length = len(input_text.split()[-1])
    selected_word = event.widget.cget("text").lower()

    if input_length == 0:
        return

    suggestions = [word for word in words if word.lower().startswith(input_text) and word.lower() != input_text]

    if suggestions:
        suggestions = suggestions[:10]  # Limit suggestions to 10

    # Remove duplicate suggestions (if the input is a complete word already present in the suggestions)
    suggestions = list(set(suggestions))

    # Clear previously displayed suggestions
    clear_previous_suggestions()

    # Display new suggestions
    for idx, suggestion in enumerate(suggestions):
        suggestion_label = tk.Label(root, text=suggestion)
        suggestion_label.pack()
        suggestion_label.bind("<Button-1>", lambda event, suggestion=suggestion: on_suggestion_click(event, suggestion))

def on_suggestion_click(event, suggestion):
    # Get the clicked suggestion
    selected_suggestion = suggestion

    # Get the current text in the entry box
    input_text = entry.get()

    # Split the input text by the last space to find the portion before the word needing completion
    input_parts = input_text.rsplit(' ', 1)
    if len(input_parts) > 1:
        new_text = input_parts[0] + ' ' + selected_suggestion  # Combine the prefix with the selected word
    else:
        new_text = selected_suggestion  # If no space, the whole text is replaced with the selected word

    # Clear the entry box and insert the selected word
    entry.delete(0, tk.END)
    entry.insert(tk.END, new_text)

    # Clear suggestions after selection
    clear_previous_suggestions()

def clear_previous_suggestions():
    # Destroy all children (suggestion labels) of the root window
    for widget in root.winfo_children():
        if isinstance(widget, tk.Label):
            widget.destroy()

# Initialize Tkinter window
root = tk.Tk()
root.title("AutoComplete Word Suggestion")
root.geometry("400x300")

# Create and place the Entry and Label widgets
entry_label = tk.Label(root, text="Enter the starting letters of a word:")
entry_label.pack()
entry = tk.Entry(root)
entry.pack()

# Load words from a text file
with open('C:\\Users\\Vivek Doshi\\Desktop\\Python\\dictionary 2.txt', 'r') as file:
    words = file.read().splitlines()

# Bind the KeyRelease event to the autocomplete function
entry.bind("<KeyRelease>", autocomplete)

# Start the GUI main loop
root.mainloop()
