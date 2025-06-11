Vòng lặp xử lý , lọc tệp có đuôi png,jpg, jpeg
for filename in os.listdir(image_folder):
    if filename.endswith(('.png', '.jpg', '.jpeg')):
        img_path = os.path.join(image_folder, filename)
        img = cv2.imread(img_path)


Khử nhiễu và chuyển sang ảnh xám
Chuyển đổi hình ảnh đã khử nhiễu từ không gian màu BGR (màu) sang ảnh xám (grayscale).

denoised_img = cv2.GaussianBlur(img, (5, 5), 0)
gray_img = cv2.cvtColor(denoised_img, cv2.COLOR_BGR2GRAY)


Tính toán đạo hàm ảnh theo chiều ngang (phát hiện cạnh dọc).
Kiểu dữ liệu đầu ra là float 64-bit
chỉ đạo hàm tính theo chiều X
sobelx = cv2.Sobel(gray_img, cv2.CV_64F, 1, 0, ksize=5)

tính toán đạo hàm ảnh theo chiều dọc (phát hiện cạnh ngang).
chỉ đạo hàm tính theo chiều Y
sobely = cv2.Sobel(gray_img, cv2.CV_64F, 0, 1, ksize=5)

Lấy giá trị tuyệt đối của các đạo hàm
sobel_combined = cv2.bitwise_or(np.uint8(np.absolute(sobelx)), np.uint8(np.absolute(sobely)))
cv2.imwrite(os.path.join(output_folder, f'sobel_{filename}'), sobel_combined)


Phát hiện cạnh bằng thuật toán Laplacian
 Lấy giá trị tuyệt đố
laplacian = cv2.Laplacian(gray_img, cv2.CV_64F)
laplacian_abs = np.uint8(np.absolute(laplacian))
cv2.imwrite(os.path.join(output_folder, f'laplacian_{filename}'), laplacian_abs)


Phát hiện cạnh bằng thuật toán Canny
canny_edges = cv2.Canny(gray_img, threshold1=100, threshold2=200)
cv2.imwrite(os.path.join(output_folder, f'canny_{filename}'), canny_edges)

