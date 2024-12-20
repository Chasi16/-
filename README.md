
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ประเมินความแรงของการออกกำลังกาย</title>
    <style>
        body {
            background-color: pink;
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        h1 {
            text-align: center;
            color: white;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .form-group {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .btn {
            background-color: #ff66b2;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
        }
        .btn:hover {
            background-color: #ff3385;
        }
        .result {
            font-size: 18px;
            color: green;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <h1>ประเมินความแรงของการออกกำลังกาย</h1>

    <div class="container">
        <div class="form-group">
            <label for="age">กรุณากรอกอายุของคุณ:</label>
            <input type="number" id="age" placeholder="กรุณากรอกอายุ" required>
        </div>

        <div class="form-group">
            <label for="heart-rate">กรุณากรอกชีพจรขณะหรือหลังออกกำลังกาย (ครั้ง/นาที):</label>
            <input type="number" id="heart-rate" placeholder="กรุณากรอกชีพจร" required>
        </div>

        <button class="btn" onclick="evaluateExercise()">ประเมินผล</button>

        <div id="result" class="result"></div>
    </div>

    <script>
        function evaluateExercise() {
            const age = parseInt(document.getElementById('age').value);
            const heartRate = parseInt(document.getElementById('heart-rate').value);
            let result = '';

            if (isNaN(age) || isNaN(heartRate) || age <= 0 || heartRate <= 0) {
                result = 'กรุณากรอกข้อมูลอายุและชีพจรที่ถูกต้อง!';
            } else {
                let maxHeartRate = 220 - age;  // ชีพจรสูงสุด
                let targetMin = (60 / 100) * maxHeartRate;  // 60% ของชีพจรสูงสุด
                let targetMax = (80 / 100) * maxHeartRate;  // 80% ของชีพจรสูงสุด

                // ตรวจสอบว่าชีพจรของผู้ใช้ตรงกับช่วงที่คำนวณได้หรือไม่
                if (heartRate >= targetMin && heartRate <= targetMax) {
                    result = 'มีความแรงเพียงพอแล้ว ทำได้ดีมากค่ะ';
                } else if (heartRate < targetMin) {
                    result = 'ยังมีความแรงไม่พอ พยายามอีกนิดนะคะ';
                } else {
                    result = 'มีความแรงมากกว่าปกติ อย่าหักโหมเกินไปนะคะ';
                }

                // แสดงชีพจรเป้าหมายตามช่วงที่คำนวณได้
                result += `<br><br>ชีพจรเป้าหมายสำหรับคุณ (อายุ ${age} ปี): ${Math.round(targetMin)} - ${Math.round(targetMax)} ครั้ง/นาที`;
            }

            document.getElementById('result').innerHTML = result;
        }
    </script>

</body>
</html>
