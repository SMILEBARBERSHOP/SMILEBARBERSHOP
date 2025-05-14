**import zipfile
import os
from shutil import copyfile

# Define paths
output_dir = "/mnt/data/smile_barbershop_site"
images_dir = os.path.join(output_dir, "images")
os.makedirs(images_dir, exist_ok=True)

# Mapping original filenames to friendly names (optional but clearer for HTML)
image_files = {
    "file-ShsjSfPsXza1E2TzRMWfju": "lobby.jpg",
    "file-8hic8imjBdLdELXeqvr9EG": "massage_room.jpg",
    "file-TZ9s2WTcAbDWGKuAbwMmPf": "shampoo_room.jpg",
    "file-CaUtUouAKXeCxjzjgoSBnJ": "front.jpg"
}

# Copy uploaded files to the new images directory with proper names
for file_id, filename in image_files.items():
    src = f"/mnt/data/{file_id}"
    dst = os.path.join(images_dir, filename)
    copyfile(src, dst)

# HTML content with correct image paths
html_content = """
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>스마일 이발소 - Smile Barbershop</title>
  <style>
    body { font-family: sans-serif; line-height: 1.6; padding: 20px; max-width: 900px; margin: auto; }
    h1, h2 { color: #333; }
    .gallery img { width: 100%; max-width: 400px; margin: 10px; border-radius: 8px; }
    .gallery { display: flex; flex-wrap: wrap; gap: 10px; justify-content: center; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; }
    table, th, td { border: 1px solid #ccc; }
    th, td { padding: 10px; text-align: left; }
    .highlight { background-color: #f8f8f8; }
  </style>
</head>
<body>
  <h1>스마일 이발소 (SMILE BARBERSHOP)</h1>
  <p>편안하고 전문적인 서비스를 제공하는 스마일 이발소입니다.</p>

  <h2>📸 시설 안내</h2>
  <div class="gallery">
    <img src="images/front.jpg" alt="전면" />
    <img src="images/lobby.jpg" alt="로비" />
    <img src="images/massage_room.jpg" alt="마사지실" />
    <img src="images/shampoo_room.jpg" alt="샴푸방" />
  </div>

  <h2>🕒 영업시간</h2>
  <p>매일 오전 9:00 ~ 오후 9:00</p>

  <h2>💈 서비스 코스 및 가격</h2>
  <table>
    <thead>
      <tr class="highlight">
        <th>코스</th>
        <th>내용</th>
        <th>가격</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>30분 면도 코스</td>
        <td>면도, 얼굴마사지, 세안, 샴푸</td>
        <td>250,000 VND</td>
      </tr>
      <tr>
        <td>60분 코스</td>
        <td>세족, 면도, 귀소지, 얼굴마사지, 오이팩, 손발톱정리, 샴푸, 세안, 로션</td>
        <td>400,000 VND</td>
      </tr>
      <tr>
        <td>90분 코스</td>
        <td>세족, 발각질제거, 면도, 귀소지, 얼굴마사지, 오이팩, 손발톱정리, 전신마사지, 샴푸, 세안, 로션</td>
        <td>500,000 VND</td>
      </tr>
      <tr>
        <td>120분 코스</td>
        <td>세족, 발각질제거, 면도, 귀소지, 얼굴마사지, 오이팩, 손발톱정리, 전신마사지, 샴푸, 세안, 로션</td>
        <td>600,000 VND</td>
      </tr>
    </tbody>
  </table>
  <p>※ 전 코스 4핸드 추가 시 +200,000 VND / VIP 추가 시 +200,000 VND</p>

  <footer style="margin-top:40px; text-align:center; font-size: 0.9em; color: #666;">
    © 2025 SMILE BARBERSHOP
  </footer>
</body>
</html>
"""

# Save HTML
html_path = os.path.join(output_dir, "index.html")
with open(html_path, "w", encoding="utf-8") as f:
    f.write(html_content)

# Zip the folder
zip_path = "/mnt/data/smile_barbershop_site.zip"
with zipfile.ZipFile(zip_path, "w") as zipf:
    for root, _, files in os.walk(output_dir):
        for file in files:
            full_path = os.path.join(root, file)
            arcname = os.path.relpath(full_path, output_dir)
            zipf.write(full_path, arcname)

zip_path
**
