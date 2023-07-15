import tkinter as tk
from tkinter import filedialog, messagebox, Toplevel, Label, Entry, Button
from PIL import Image, ImageTk, ImageFilter

# إنشاء النافذة الرئيسية للتطبيق
root = tk.Tk()
root.title("تحويل الصور")
root.geometry("500x800")

# تحميل الصورة المحددة
def load_image():
    global selected_image, image_label, imageToResetLater
    file_path = filedialog.askopenfilename()
    try:
        selected_image = Image.open(file_path)
        imageToResetLater = selected_image
        display_image(selected_image)
        # إظهار معلومات الصورة
        image_label.configure(text="الصورة المحددة: " + file_path)
    except:
        messagebox.showerror("خطأ", "فشل تحميل الصورة")

# عرض الصورة في النافذة الرئيسية
def display_image(image):
    global image_canvas, image_tk
    image_tk = ImageTk.PhotoImage(image)
    if image_canvas is not None:
        image_canvas.destroy()
    image_canvas = tk.Canvas(root, width=image.width, height=image.height)
    image_canvas.create_image(0, 0, anchor=tk.NW, image=image_tk)
    image_canvas.pack()

# تحويل الصورة إلى أبيض وأسود
def bw_image():
    global selected_image
    bw = selected_image.convert('L')
    selected_image = bw # update the selected_image variable
    display_image(selected_image)
    # عرض العملية التي تم تطبيقها على الصورة
    image_label.configure(text="تم تحويل الصورة إلى أبيض وأسود")

# تطبيق التغبيش على الصورة
def blur_image():
    global selected_image
    # إنشاء نافذة  لإدخال مستوى التغبيش
    blur_window = Toplevel(root)
    blur_window.title("تطبيق البلر")
    blur_window.geometry("300x200")

    # إنشاء عنصر الإدخال لإدخال مستوى التغبيش
    blur_label = Label(blur_window, text="أدخل مستوى التغبيش:")
    blur_label.pack(pady=10)
    blur_entry = Entry(blur_window)
    blur_entry.pack()

    # إنشاء زر التأكيد
    confirm_button = Button(blur_window, text="تطبيق",
                            command=lambda: apply_blur(blur_window, blur_entry.get()))
    confirm_button.pack(pady=10)

def apply_blur(blur_window, blur_level):
    global selected_image
    try:
        # تحويل مستوى التغبيش إلى رقم صحيح
        blur_level = int(blur_level)
        # تطبيق  التغبيش على الصورة وعرض الصورة
        blurred = selected_image.filter(ImageFilter.GaussianBlur(blur_level))
        selected_image = blurred  #  selected_image
        display_image(selected_image)
        # تحديث الصورة  لعرض العملية التي تم تطبيقها
        image_label.configure(text=f"تم تطبيق بلر بمستوى تغبيش {blur_level}")
        # إغلاق النافذة
        blur_window.destroy()
    except:
        messagebox.showerror("خطأ", "فشل تطبيق البلر")

# قلب الصورة
def flip_image():
    global selected_image
    flipped = selected_image.transpose(Image.FLIP_LEFT_RIGHT)
    selected_image = flipped # تحديث متغير selected_image
    display_image(selected_image)
    # عرض العملية التي تم تطبيقها على الصورة المقلوبه
    image_label.configure(text="تم تطبيق قلب الصورة")

#تغيير حجم الصورة
def resize_image():
    global selected_image
    # إنشاء نافذة المربع  لإدخال حجم التغيير
    resize_window = Toplevel(root)
    resize_window.title("تغيير حجم الصورة")
    resize_window.geometry("300x200")

    # إنشاء عنصر الإدخال لإدخال حجم التغيير
    resize_label = Label(resize_window, text="أدخل حجم التغيير:")
    resize_label.pack(pady=10)
    resize_entry = Entry(resize_window)
    resize_entry.pack()

    # إنشاء زر التأكيد لتطبيق التغيير
    confirm_button = Button(resize_window, text="تطبيق",
                            command=lambda: apply_resize(resize_window, resize_entry.get()))
    confirm_button.pack(pady=10)

def apply_resize(resize_window, resize_size):
    global selected_image
    try:
        # تحويل حجم التغيير إلى رقم صحيح
        resize_size = int(resize_size)
        # تطبيق التغيير على الصورة وعرض الصورة المصغرة
        resized = selected_image.resize((resize_size, resize_size))
        selected_image = resized # تحديث متغير selected_image
        display_image(selected_image)
        # تحديث الصورة لعرض العملية التي تم تطبيقها
        image_label.configure(text=f"تم تغيير الصورة إلى حجم {resize_size}")
        # إغلاق نافذة المربع
        resize_window.destroy()
    except:
        messagebox.showerror("خطأ", "فشل تغيير حجم الصورة")

def reset_image():
    global selected_image
    selected_image = imageToResetLater
    display_image(selected_image)
    # Update the status label to show that the image has been reset
    image_label.configure(text="تم إعادة تعيين الصورة الأصلية")

# إنشاء عنصر  لعرض معلومات الصورة المحددة
image_label = Label(root, text="لم يتم تحميل الصورة بعد", font=("Arial", 12))
image_label.pack(pady=10)

# إنشاء زر لتحميل الصورة
load_button = Button(root, text="تحميل الصورة", command=load_image)
load_button.pack(pady=10)

# إنشاء زر لتحويل الصورة إلى أبيض وأسود
bw_button = Button(root, text="تحويل الصورة إلى أبيض وأسود", command=bw_image)
bw_button.pack(pady=10)

# إنشاء زر لتطبيق بلر على الصورة
blur_button = Button(root, text="تطبيق بلر على الصورة", command=blur_image)
blur_button.pack(pady=10)

# إنشاء زر لقلب الصورة
flip_button = Button(root, text="قلب الصورة", command=flip_image)
flip_button.pack(pady=10)

# إنشاء زر لتغيير حجم الصورة
resize_button = Button(root, text="تغيير حجم الصورة", command=resize_image)
resize_button.pack(pady=10)

# إنشاء زر لإعادة الصورة الأصلية
reset_button = Button(root, text="إعادة الصورة الأصلية", command=reset_image)
reset_button.pack(pady=10)

# إنشاء متغيرات للاحتفاظ بالصورة المحددة  في النافذة الرئيسية
selected_image = None
image_canvas = None
image_tk = None
imageToResetLater = None

# تشغيل النافذة الرئيسية
root.mainloop()
