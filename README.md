Câu 1: Điều chỉnh màu xanh lá và màu xanh về 0, chỉ giữ màu đỏ
red_image = arr.copy()
red_image[:, :, 1] = 0  # G
red_image[:, :, 2] = 0  # B

Điều chỉnh màu đỏ và màu xanh dương về 0, giữ lại màu xanh lá
green_image = arr.copy() 
green_image[:, :, 0] = 0  # R
green_image[:, :, 2] = 0  # B

Điều chỉnh màu đỏ và màu xanh lá về 0, giữ lại màu xanh dương
blue_image = arr.copy()
blue_image[:, :, 0] = 0  # R
blue_image[:, :, 1] = 0  # G

Hiển thị 3 ảnh 
plt.figure(figsize=(12, 4))
plt.subplot(1, 3, 1)
plt.imshow(red_image)
plt.subplot(1, 3, 2)
plt.imshow(green_image)
plt.subplot(1, 3, 3)
plt.imshow(blue_image)
plt.tight_layout()
plt.show()



Câu 2: + mở ảnh và chuyển ảnh thành mảng
image = Image.open('bird.png')
arr = np.array(image)

+ Hoán đổi kênh màu
swapped = arr[..., [2, 1, 0]]

+ Hiển thị ảnh
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 2)
plt.imshow(swapped)
plt.tight_layout()
plt.show() 

Câu 3: + Mở ảnh và chuyển ảnh RGB
image = Image.open('bird.png').convert('RGB')
arr = np.array(image) / 255.0

+ Tạo mảng trống cùng kích thước với ảnh để chứa giá trị HSV
hsv = np.zeros_like(arr)
for i in range(arr.shape[0]):
    for j in range(arr.shape[1]):
        hsv[i, j] = colorsys.rgb_to_hsv(arr[i, j, 0], arr[i, j, 1], arr[i, j, 2])

+ Tách riêng 3 kênh H, S, V
H = (hsv[:, :, 0] * 255).astype(np.uint8)
S = (hsv[:, :, 1] * 255).astype(np.uint8)
V = (hsv[:, :, 2] * 255).astype(np.uint8)

+ Lưu và hiển thị 3 ảnh
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(H, cmap='hsv')
plt.title('Hue')

plt.subplot(1, 3, 2)
plt.imshow(S, cmap='gray')
plt.title('Saturation')

plt.subplot(1, 3, 3)
plt.imshow(V, cmap='gray')
plt.title('Value')

plt.tight_layout()
plt.show()

Câu 4:
+ Đọc ảnh và chuẩn hoá, sau đó chuyển từng điểm ảnh từ RGB sang HSV
image = Image.open('bird.png').convert('RGB')
arr = np.array(image) / 255.0
hsv = np.zeros_like(arr)

+ Giá trị Hue được chia 3 để thay đổi tông màu, Value giảm 25% để làm ảnh tối hơn.
for i in range(arr.shape[0]):
    for j in range(arr.shape[1]):
        h, s, v = colorsys.rgb_to_hsv(arr[i, j, 0], arr[i, j, 1], arr[i, j, 2])
        h = h / 3
        v = v * 0.75
        hsv[i, j] = colorsys.hsv_to_rgb(h, s, v)

+ Ảnh được chuyển lại sang RGB và hiển thị kết quả sau khi điều chỉnh màu.
rgb_new = (hsv * 255).astype(np.uint8)

plt.imshow(rgb_new)
plt.axis('off')
plt.show()

