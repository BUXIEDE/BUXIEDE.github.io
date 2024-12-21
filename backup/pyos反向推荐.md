你敢信，一个4.5kb的程序能够包含以下功能？！
计算器
计算器应该是每个电子项目必备的了，计算器的功能也是朴实无华，你也许会问0.1+0.2能不能算？笑死，我们没有小数点！
记事本（我觉得不用介绍）
就是notepad，他不如你电脑自带的
运行Python文件
不用看，不如你的文件管理器
下载链接：https://pan.quark.cn/s/593002d2f447
代码是
'''python
import tkinter as tk
from tkinter import filedialog， messagebox
import subprocess

声明全局变量
calc_window = 无
notepad_window = 无

计算器功能
def open_calculator（）：

如果 calc_window 为 None，则全局calc_window：
calc_window = tk。Toplevel（root）
calc_window.title（“计算器”）
calc_window.geometry（“300x400”）

    entry = tk.Entry(calc_window, width=35, borderwidth=5)
    entry.grid(row=0, column=0, columnspan=4, padx=10, pady=10)
    
    def button_click(number):
        current = entry.get()
        entry.delete(0, tk.END)
        entry.insert(0, str(current) + str(number))
    
    def button_clear():
        entry.delete(0, tk.END)
    
    def button_equal():
        try:
            current = entry.get()
            result = str(eval(current))
            entry.delete(0, tk.END)
            entry.insert(0, result)
        except:
            entry.delete(0, tk.END)
            entry.insert(0, "Error")
    
    buttons = [
        '7', '8', '9', '/',
        '4', '5', '6', '*',
        '1', '2', '3', '-',
        'C', '0', '=', '+']
    row_val = 1
    col_val = 0
    for button in buttons:
        if button == 'C':
            b = tk.Button(calc_window, text=button, padx=40, pady=20, command=button_clear)
        elif button == '=':
            b = tk.Button(calc_window, text=button, padx=40, pady=20, command=button_equal)
        else:
            b = tk.Button(calc_window, text=button, padx=37, pady=20, command=lambda button=button: button_click(button))
        b.grid(row=row_val, column=col_val)
        col_val += 1
        if col_val > 3:
            col_val = 0
            row_val += 1
    calc_window.protocol("WM_DELETE_WINDOW", lambda: (update_taskbar("计算器", False), calc_window.withdraw()))
    update_taskbar("计算器", True)
else:
    calc_window.deiconify()
记事本功能
def open_notepad（）：

如果 notepad_window 为 None，则全局notepad_window：
notepad_window = tk。Toplevel（根）
notepad_window.title（“记事本”）
notepad_window.geometry（“400x300”）

    text_area = tk.Text(notepad_window)
    text_area.pack(expand=True, fill='both')
    notepad_window.protocol("WM_DELETE_WINDOW", lambda: (update_taskbar("记事本", False), notepad_window.withdraw()))
    update_taskbar("记事本", True)
else:
    notepad_window.deiconify()
关于对话框
def about（）：
messagebox.showinfo（“关于”， “制作人：一只不屑的py。2024")

运行Python脚本
def run_python_script（）：
file_path = filedialog.askopenfilename（filetypes=[（“Python files”， “*.py”）]）
如果file_path：
try：
subprocess.run（[“python”， file_path]， check=True）
except subprocess.CalledProcessError as e：
messagebox.showerror（“错误”， f“运行脚本失败： {e}”）

更新任务栏
def update_taskbar（title， add=True）：
对于 taskbar.winfo_children（） 中的小部件：
widget.pack_forget（）
if add：
taskbar_label = tk.标签（任务栏， text=title， bg='gray'， width=20）
taskbar_label.pack（side='left'， padx=5）
taskbar_label.bind（“”， lambda 事件， title=title： toggle_window（title））

切换窗口显示/隐藏
def toggle_window（title）：
如果 title == “计算器” 且 calc_window 不是 None：
calc_window.deiconify（）
elif title == “记事本” 且 notepad_window 不是 None：
notepad_window.deiconify（）

创建主窗口
根 = tk。Tk（）
root.title（“主窗口”）

创建任务栏
任务栏 = TK。Frame（根， bg='gray'， height=30）
taskbar.pack（side='top'， fill='x'）

创建DOCK栏
码头 = TK。frame（根， bg='蓝色'， 高度=100）
dock.pack（side='bottom'， fill='x'）

创建DOCK栏中的按钮
calculator_button = tk。Button（dock， text=“计算器”， command=open_calculator）
notepad_button = tk.Button（dock， text=“记事本”， command=open_notepad）
run_script_button = tk.Button（dock， text=“运行Python脚本”， command=run_python_script）
about_button = tk.按钮（dock， text=“关于”， command=about）

布局DOCK栏中的按钮
calculator_button.pack（side='left'， padx=10， pady=10）
notepad_button.pack（side='left'， padx=10， pady=10）
run_script_button.pack（side='left'， padx=10， pady=10）
about_button.pack（side='right'， padx=10， pady=10）

运行主循环
root.mainloop（）
'''