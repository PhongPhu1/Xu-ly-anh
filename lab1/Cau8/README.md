
Khử nhiễu
denoised_img = cv2.GaussianBlur(img, (5, 5), 0)

Tách và xáo trộn kênh màu. Tạo một danh sách chứ 3 kênh mà dã tách. Xáo trộn ngẫu nhiên các kênh màu
b, g, r = cv2.split(denoised_img)
channels = [b, g, r]
random.shuffle(channels)
random_rgb_img = cv2.merge(channels)

