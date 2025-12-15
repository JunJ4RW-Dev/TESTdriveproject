# COMproject final
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title>File Summarizer</title>
</head>
<body>
  <h2>อัปโหลดไฟล์เพื่อสรุป</h2>

  <input type="file" id="file" />
  <button onclick="upload()">สรุปเนื้อหา</button>

  <pre id="result"></pre>

  <script>
    async function upload() {
      const fileInput = document.getElementById("file");
      const formData = new FormData();
      formData.append("file", fileInput.files[0]);

      const res = await fetch("/summarize", {
        method: "POST",
        body: formData
      });

      const data = await res.json();
      document.getElementById("result").textContent = data.summary;
    }
  </script>
</body>
</html>

