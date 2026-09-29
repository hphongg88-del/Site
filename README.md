<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ôn Tập Công Thức Toán 11 & 12</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
        }
        .quiz-card {
            background: white;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 600px;
            padding: 25px;
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid #f0f2f5;
            padding-bottom: 15px;
            margin-bottom: 20px;
        }
        .category {
            font-size: 0.85rem;
            font-weight: bold;
            color: #007bff;
            text-transform: uppercase;
            background: #e6f0ff;
            padding: 4px 10px;
            border-radius: 20px;
        }
        .score {
            font-size: 0.9rem;
            color: #555;
            font-weight: 600;
        }
        .question {
            font-size: 1.15rem;
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 20px;
            line-height: 1.4;
        }
        .options-grid {
            display: grid;
            gap: 10px;
        }
        .option-btn {
            background: #f8f9fa;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            padding: 12px 15px;
            font-size: 1rem;
            text-align: left;
            cursor: pointer;
            transition: all 0.2s ease;
            color: #333;
        }
        .option-btn:hover:not([disabled]) {
            background: #e2e6ea;
            border-color: #adb5bd;
        }
        .option-btn.correct {
            background-color: #d4edda !important;
            border-color: #28a745 !important;
            color: #155724 !important;
            font-weight: bold;
        }
        .option-btn.wrong {
            background-color: #f8d7da !important;
            border-color: #dc3545 !important;
            color: #721c24 !important;
        }
        .explanation {
            margin-top: 15px;
            padding: 12px;
            border-radius: 6px;
            background-color: #e9ecef;
            font-size: 0.95rem;
            display: none;
            color: #495057;
        }
        .next-btn {
            margin-top: 20px;
            width: 100%;
            padding: 12px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            display: none;
            transition: background 0.2s;
        }
        .next-btn:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>

<div class="quiz-card">
    <div class="header">
        <span class="category" id="category">Danh mục</span>
        <span class="score" id="score">Điểm: 0</span>
    </div>
    
    <div class="question" id="question">Đang tải câu hỏi...</div>
    
    <div class="options-grid" id="options"></div>
    
    <div class="explanation" id="explanation"></div>
    
    <button class="next-btn" id="next-btn" onclick="nextQuestion()">Câu Tiếp Theo ➔</button>
</div>

<script>
const quizData = [
    // Lượng giác 11
    {
        category: "Lượng Giác 11",
        question: "Công thức nghiệm của sin x = 0 là gì?",
        options: ["x = kπ", "x = π/2 + k2π", "x = k2π", "x = π/2 + kπ"],
        answer: 0,
        explanation: "sin x = 0 ⇔ x = kπ (k ∈ Z)."
    },
    {
        category: "Lượng Giác 11",
        question: "Công thức nghiệm của cos x = 0 là gì?",
        options: ["x = k2π", "x = π/2 + kπ", "x = π + k2π", "x = kπ"],
        answer: 1,
        explanation: "cos x = 0 ⇔ x = π/2 + kπ (k ∈ Z)."
    },
    {
        category: "Lượng Giác 11",
        question: "Công thức tổng quát nghiệm của cos x = cos α là gì?",
        options: [
            "x = α + k2π hoặc x = π - α + k2π",
            "x = α + kπ hoặc x = -α + kπ",
            "x = ±α + k2π",
            "x = ±α + kπ"
        ],
        answer: 2,
        explanation: "cos đối ⇔ x = ±α + k2π (k ∈ Z)."
    },
    // Thể tích & Hình học 11
    {
        category: "Hình Học 11",
        question: "Công thức tính thể tích khối chóp là gì?",
        options: ["V = B . h", "V = 1/2 . B . h", "V = 1/3 . B . h", "V = 4/3 . B . h"],
        answer: 2,
        explanation: "Khối chóp / khối nón luôn có hệ số 1/3: V = 1/3 . B . h (với B là diện tích đáy, h là chiều cao)."
    },
    {
        category: "Hình Học 11",
        question: "Diện tích của tam giác đều cạnh 'a' bằng bao nhiêu?",
        options: ["(a²√3) / 2", "(a²√3) / 4", "a²√2", "(a²√2) / 4"],
        answer: 1,
        explanation: "S = (a²√3) / 4."
    },
    {
        category: "Hình Học 11",
        question: "Chiều cao của tam giác đều cạnh 'a' bằng bao nhiêu?",
        options: ["(a√3) / 2", "(a√2) / 2", "a√3", "(a√3) / 4"],
        answer: 0,
        explanation: "h = (a√3) / 2."
    },
    {
        category: "Hình Học 11",
        question: "Độ dài đường chéo của hình vuông cạnh 'a' là bao nhiêu?",
        options: ["a√3", "a√2", "2a", "a²/2"],
        answer: 1,
        explanation: "Đường chéo hình vuông = a√2."
    },
    // Hàm số 12
    {
        category: "Hàm Số 12",
        question: "Hàm số y = f(x) đồng biến trên K khi nào?",
        options: ["f'(x) ≤ 0 với mọi x ∈ K", "f'(x) ≥ 0 với mọi x ∈ K", "f'(x) = 0 với mọi x ∈ K", "f'(x) đổi dấu trên K"],
        answer: 1,
        explanation: "Hàm số đồng biến khi đạo hàm f'(x) ≥ 0 (dấu bằng chỉ xảy ra tại hữu hạn điểm)."
    },
    {
        category: "Hàm Số 12",
        question: "Đồ thị hàm số phân thức có tiệm cận ngang y = 0 khi nào?",
        options: [
            "Bậc của Tử lớn hơn Bậc của Mẫu",
            "Bậc của Tử bằng Bậc của Mẫu",
            "Bậc của Tử nhỏ hơn Bậc của Mẫu",
            "Mẫu số không có nghiệm"
        ],
        answer: 2,
        explanation: "Khi x → ∞, nếu Bậc Tử < Bậc Mẫu thì lim y = 0 ⇒ Tiệm cận ngang y = 0."
    },
    // Xác suất 11
    {
        category: "Xác Suất 11",
        question: "Khi chọn k phần tử từ n phần tử KHÔNG sắp xếp thứ tự, ta dùng công thức nào?",
        options: ["Hoán vị (Pn)", "Chỉnh hợp (An^k)", "Tổ hợp (Cn^k)", "Quy tắc nhân"],
        answer: 2,
        explanation: "Chọn không xếp thứ tự dùng Tổ hợp Cn^k. Chọn có xếp thứ tự dùng Chỉnh hợp An^k."
    }
];

let currentQuestionIndex = 0;
let score = 0;

function loadQuestion() {
    const q = quizData[currentQuestionIndex];
    document.getElementById("category").innerText = q.category;
    document.getElementById("question").innerText = `Câu ${currentQuestionIndex + 1}: ${q.question}`;
    
    const optionsContainer = document.getElementById("options");
    optionsContainer.innerHTML = "";
    
    document.getElementById("explanation").style.display = "none";
    document.getElementById("next-btn").style.display = "none";
    
    q.options.forEach((opt, index) => {
        const btn = document.createElement("button");
        btn.className = "option-btn";
        btn.innerText = opt;
        btn.onclick = () => checkAnswer(index, btn);
        optionsContainer.appendChild(btn);
    });
}

function checkAnswer(selectedIndex, selectedBtn) {
    const q = quizData[currentQuestionIndex];
    const buttons = document.querySelectorAll(".option-btn");
    
    buttons.forEach(btn => btn.disabled = true);
    
    if (selectedIndex === q.answer) {
        selectedBtn.classList.add("correct");
        score += 10;
        document.getElementById("score").innerText = `Điểm: ${score}`;
    } else {
        selectedBtn.classList.add("wrong");
        buttons[q.answer].classList.add("correct");
    }
    
    const expBox = document.getElementById("explanation");
    expBox.innerText = "Giải thích: " + q.explanation;
    expBox.style.display = "block";
    
    document.getElementById("next-btn").style.display = "block";
}

function nextQuestion() {
    currentQuestionIndex = (currentQuestionIndex + 1) % quizData.length;
    loadQuestion();
}

// Khởi chạy câu hỏi đầu tiên
loadQuestion();
</script>

</body>
</html>
