Thiết lập dau vào và ra thư mục:

image_folder = 'exercise'
output_folder = 'khunhieu'

if not os.path.exists(output_folder):
    os.makedirs(output_folder)

Vòng lặp xử lý ảnh
Duyệt qua tất cả các ảnh trong thư mục, kiểm tra file name có  phải là tệp png, jpg, jpeg hay không. Tạo dường dẫn  tệp hình anh. Sau đó đọc hình anh từ dường dẫn

for filename in os.listdir(image_folder):
    if filename.endswith(('.png', '.jpg', '.jpeg')):
        img_path = os.path.join(image_folder, filename)
        img = cv2.imread(img_path)


Làm mờ trung bình:
avg_blur = cv2.blur(img, (5, 5))
cv2.imwrite(os.path.join(output_folder, f'avg_{filename}'), avg_blur)


Làm mờ Gaussian
gaussian_blur = cv2.GaussianBlur(img, (5, 5), 0)
cv2.imwrite(os.path.join(output_folder, f'gaussian_{filename}'), gaussian_blur)


Làm mờ trung vị
median_blur = cv2.medianBlur(img, 5)
cv2.imwrite(os.path.join(output_folder, f'median_{filename}'), median_blur)


Bộ lọc song phương
bilateral_filter = cv2.bilateralFilter(img, 9, 75, 75)
cv2.imwrite(os.path.join(output_folder, f'bilateral_{filename}'), bilateral_filter)



