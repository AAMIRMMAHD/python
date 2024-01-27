from tkinter import *
from tkinter import messagebox

root = Tk()
root.geometry('800x500+500+200')
root.resizable(0, 0)
root.title('Student Management System')
root.configure(bg='#808080')

button_width = 15
button_padding_y = 5
def insert():
    name = entry_name.get()
    score = entry_score.get()
    number = entry_number.get()

    lst_student.insert(END, f'Name: {name}, Score: {score}, Number: {number}')
    clear()
def delete():
    index = lst_student.curselection()
    result = messagebox.askquestion('Delete', 'Are you sure you want to delete?')
    if result == 'yes':
        lst_student.delete(index)
def fetch():
    index = lst_student.curselection()
    data = lst_student.get(index)
    item = data.split(',')
    entry_name.delete(0, END)
    entry_score.delete(0, END)
    entry_number.delete(0, END)
    entry_name.insert(0, item[0].split(':')[1].strip())
    entry_score.insert(0, item[1].split(':')[1].strip())
    entry_number.insert(0, item[2].split(':')[1].strip())
def clear():
    entry_name.delete(0, END)
    entry_score.delete(0, END)
    entry_number.delete(0, END)
    entry_name.focus_set()
def exit_program():
    root.destroy()
def evaluate_score():
    selected_index = lst_student.curselection()
    if selected_index:
        selected_item = lst_student.get(selected_index)
        try:
            score = int(eval(selected_item.split(':')[2].strip().split(',')[0]))
            result = evaluate_score_status(score)
            messagebox.showinfo("Score Evaluation Result", f"Score: {score}, Status: {result}")
        except ValueError:
            messagebox.showerror("Error", "Invalid score.")
    else:
        messagebox.showerror("Error", "Please select an item from the list.")
def evaluate_score_status(score):
    if 0 <= score < 10:
        return "Very Bad"
    elif 10 <= score < 12:
        return "Bad"
    elif 12 <= score < 15:
        return "Not Good"
    elif 15 <= score < 17:
        return "Good"
    elif 17 <= score <= 20:
        return "Very Good"
    else:
        return "Invalid score"
root_bg_label = Label(root, text='', bg='#808080')
root_bg_label.place(relwidth=1, relheight=1)
btn_evaluate = Button(root, text='Evaluate Score', font='arial 14 bold', command=evaluate_score, width=button_width)
btn_evaluate.place(x=550, y=50 + button_padding_y)
lbl_name = Label(root, text='Name: ', font='arial 14 bold', bg='#808080', fg='white')
lbl_name.place(x=40, y=90)
entry_name = Entry(root, font='arial 12 bold')
entry_name.place(x=200, y=90)
lbl_score = Label(root, text='Score: ', font='arial 14 bold', bg='#808080', fg='white')
lbl_score.place(x=40, y=130)
entry_score = Entry(root, font='arial 12 bold')
entry_score.place(x=200, y=130)
lbl_number = Label(root, text='Number: ', font='arial 14 bold', bg='#808080', fg='white')
lbl_number.place(x=40, y=170)
entry_number = Entry(root, font='arial 12 bold')
entry_number.place(x=200, y=170)
lst_student = Listbox(root, width=40, height=10, bg='#808080', fg='white', font='arial 14 bold')
lst_student.place(x=40, y=220)
btn_insert = Button(root, text='Insert', font='arial 14 bold', command=insert, width=button_width)
btn_insert.place(x=550, y=90 + button_padding_y)
btn_delete = Button(root, text='Delete', font='arial 14 bold', command=delete, width=button_width)
btn_delete.place(x=550, y=130 + button_padding_y)
btn_fetch = Button(root, text='Fetch', font='arial 14 bold', command=fetch, width=button_width)
btn_fetch.place(x=550, y=170 + button_padding_y)
btn_clear = Button(root, text='Clear', font='arial 14 bold', command=clear, width=button_width)
btn_clear.place(x=550, y=210 + button_padding_y)
btn_exit = Button(root, text='Exit', font='arial 14 bold', command=exit_program, width=button_width)
btn_exit.place(x=550, y=250 + button_padding_y)
root.mainloop()

