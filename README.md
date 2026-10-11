# BIỂU ĐỒ TỰ ĐÁNH GIÁ NĂNG LỰC ICT CỦA BẢN THÂN TRONG DẠY HỌC
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kết quả tự đánh giá</title>

  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 12px;
      font-family: Arial, sans-serif;
      background: #ffffff;
    }

    .chart-container {
      position: relative;
      width: 100%;
      height: 420px;
    }

    @media (max-width: 600px) {
      .chart-container {
        height: 390px;
      }
    }
  </style>
</head>

<body>

<div class="chart-container">
  <canvas id="myChart"></canvas>
</div>

<script>
  // ======================================
  // 1. TÊN 5 NHÓM
  // ======================================

  const tenNhom = [
    ["Khai thác thông tin,", "dữ liệu và phần mềm", "dạy học"],
    ["Hợp tác và giao tiếp", "trong môi trường số"],
    ["Sáng tạo nội dung số", "và an toàn số"],
    ["Học tập nâng cao", "kĩ năng số"],
    ["Ứng dụng CNTT", "trong dạy học"]
  ];

  // ======================================
  // 2. NỘI DUNG HIỂN THỊ KHI RÊ CHUỘT
  // ======================================

  const noiDung = [
    [
      "Xác định nhu cầu và tìm kiếm thông tin, dữ liệu, phần mềm.",
      "Đánh giá thông tin, dữ liệu, phần mềm và sử dụng chúng.",
      "Quản lý và lưu trữ thông tin, dữ liệu, phần mềm."
    ],
    [
      "Nhận thức các chuẩn mực hành vi, giao tiếp, ứng xử trong môi trường số.",
      "Tham gia cộng đồng diễn đàn trực tuyến, cộng tác trong công việc thông qua công nghệ số.",
      "Thực hành vai trò người dạy và sử dụng các dịch vụ qua nền tảng số."
    ],
    [
      "Kiểm soát được dấu chân số, duy trì an toàn số, cân bằng số, nhận biết rủi ro và bảo vệ môi trường số trong quá trình sử dụng thiết bị và dịch vụ số.",
      "Bảo vệ quyền riêng tư và định danh số; xây dựng, phát triển và sử dụng nội dung số theo các cơ sở pháp lí.",
      "Tạo lập, xây dựng nội dung số, ngôn ngữ lập trình, thực hành tư duy đổi mới sáng tạo trong xây dựng nội dung số."
    ],
    [
      "Nhận biết xu thế và cơ hội của dạy học và đào tạo trực tuyến.",
      "Học tập số (công cụ và phương pháp).",
      "Truy cập mở đến các nguồn tài nguyên học tập số."
    ],
    [
      "Ứng dụng trong thiết kế kế hoạch dạy học.",
      "Ứng dụng trong tổ chức dạy học.",
      "Ứng dụng trong kiểm tra, đánh giá."
    ]
  ];

  // ======================================
  // 3. DỮ LIỆU ĐIỂM CỦA 5 NHÓM
  // ======================================

  const duLieu = [
    [3, 2, 3],
    [3, 1, 2],
    [2, 3, 3],
    [3, 3, 3],
    [3, 2, 1]
  ];

  // ======================================
  // 4. MÀU SẮC XEN KẼ THEO NHÓM
  // Nhóm 1 xanh, nhóm 2 đỏ, nhóm 3 xanh...
  // ======================================

  const mauXanh = "#124874";
  const mauDo = "#CF373D";
  const mauHover = "#E6A23C";

  const datasets = [0, 1, 2].map(function(muc) {
    return {
      label: (muc + 1) + " điểm",

      data: duLieu.map(function(nhom) {
        return nhom[muc];
      }),

      backgroundColor: function(context) {
        return context.dataIndex % 2 === 0
          ? mauXanh
          : mauDo;
      },

      hoverBackgroundColor: mauHover,

      barPercentage: 0.95,
      categoryPercentage: 0.82,

      borderRadius: 0,
      borderSkipped: false
    };
  });

  // ======================================
  // 5. VẼ BIỂU ĐỒ
  // ======================================

  new Chart(document.getElementById("myChart"), {
    type: "bar",

    data: {
      labels: tenNhom,
      datasets: datasets
    },

    options: {
      responsive: true,
      maintainAspectRatio: false,

      layout: {
        padding: {
          top: 8,
          bottom: 5,
          left: 5,
          right: 5
        }
      },

      scales: {
        x: {
          offset: true,

          title: {
            display: true,
            text: "Các nhóm",
            padding: {
              top: 12
            }
          },

          ticks: {
            autoSkip: false,
            maxRotation: 0,
            minRotation: 0,
            align: "center",
            crossAlign: "center",
            padding: 8,

            font: {
              size: 12
            }
          },

          grid: {
            display: false
          }
        },

        y: {
          min: 0,
          max: 3,

          ticks: {
            stepSize: 1,
            precision: 0
          },

          title: {
            display: true,
            text: "Thang điểm"
          }
        }
      },

      plugins: {
        // Ẩn chú giải màu sắc bên dưới biểu đồ
        legend: {
          display: false
        },

        // ======================================
        // 6. NỘI DUNG KHI RÊ CHUỘT
        // Chỉ hiện nội dung và điểm số
        // ======================================

        tooltip: {
          enabled: true,
          displayColors: false,

          callbacks: {
            // Không hiển thị tên nhóm ở đầu hộp
            title: function() {
              return "";
            },

            // Dòng đầu: nội dung đánh giá
            // Dòng tiếp theo: điểm số
            label: function(context) {
              const indexNhom = context.dataIndex;
              const muc = context.datasetIndex;
              const diem = context.parsed.y;

              return [
                noiDung[indexNhom][muc],
                diem + " điểm"
              ];
            }
          },

          // Giới hạn chiều rộng để nội dung tự xuống dòng
          bodyFont: {
            size: 13
          },

          titleFont: {
            size: 13
          },

          padding: 10,
          boxPadding: 3
        }
      }
    }
  });
</script>

</body>
</html>
