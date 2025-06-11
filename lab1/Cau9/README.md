Khử nhiễu và chuyển đổi sang HSV
denoised_img = cv2.GaussianBlur(img, (5, 5), 0)
Chuyển RGB sang HSV
hsv_img = cv2.cvtColor(denoised_img, cv2.COLOR_BGR2HSV)
Tách hình anh thành 3 kênh riêng biệt
h, s, v = cv2.split(hsv_img)



Dịch chuyển ngẫu nhiên kênh H
Tạo một số nguyên ngẫu nhiên trong khoảng từ 0 đến 179
random_hue_shift = np.random.randint(0, 180)
Chuyển đổi kiểu dữ liệu của kênh h từ uint8 (0-255) sang int32
h = h.astype(np.int32)
h = (h + random_hue_shift) % 180
h = h.astype(np.uint8)


Gộp kênh và chuyển dổi lại sang RGB
random_hsv_img = cv2.merge([h, s, v])
final_img = cv2.cvtColor(random_hsv_img, cv2.COLOR_HSV2BGR)
