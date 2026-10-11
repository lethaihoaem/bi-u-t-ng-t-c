# bieu do tuong tac
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Biểu đồ 5 nhóm - 3 mức điểm</title>

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
        height: 360px;
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
  // 1. TÊN 5 NHÓM - BẠN CÓ THỂ TỰ ĐỔI
  // ======================================

  const tenNhom = [
    "Khai thác thông tin, dữ liệu và phần mềm dạy học.",
    "Hợp tác và giao tiếp trong môi trường số.",
    "Sáng tạo nội dung số và an toàn số.",
    "Học tập nâng cao kĩ năng số.",
    "Ứng dụng CNTT trong dạy học."
  ];

  // ======================================
  // 2. NỘI DUNG TƯƠNG ỨNG VỚI TỪNG CỘT
  // Mỗi nhóm có 3 mức: 1, 2 và 3
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
  // 3. DỮ LIỆU CHIỀU CAO CỦA 15 CỘT
  // Mỗi nhóm gồm 3 cột có giá trị 1, 2, 3
  // Bạn có thể thay đổi chiều cao nếu cần
  // ======================================

  const duLieu = [
    [3, 2, 3], // Nhóm 1
    [3, 1, 2], // Nhóm 2
    [2, 3, 3], // Nhóm 3
    [3, 3, 3], // Nhóm 4
    [3, 2, 1]  // Nhóm 5
  ];

  // ======================================
  // 4. TẠO 3 TẬP DỮ LIỆU
  // Mỗi tập tương ứng một mức điểm
  // ======================================

  const mauSac = [
    "#124874",
    "#124874",
    "#124874"
  ];

  const datasets = [0, 1, 2].map(function(muc) {
    return {
      label:  (muc + 1)+ "điểm",

      data: duLieu.map(function(nhom) {
        return nhom[muc];
      }),

      backgroundColor: mauSac[muc],

      hoverBackgroundColor: "#E6A23C",

      barPercentage: 0.95,

      categoryPercentage: 0.95,

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

      // Ba cột trong mỗi nhóm nằm cạnh nhau
      scales: {
        x: {
          stacked: false,

          grid: {
            display: false
          },

          title: {
            display: true,
            text: "Các nhóm"
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
        legend: {
          display: true,
          position: "bottom",

          labels: {
            usePointStyle: true,
            pointStyle: "rect",
            padding: 18
          }
        },

        tooltip: {
          enabled: true,
          displayColors: true,

          callbacks: {
            title: function(items) {
              const indexNhom = items[0].dataIndex;
              const muc = items[0].datasetIndex + 1;

              return tenNhom[indexNhom] + " - Mức " + muc;
            },

            label: function(context) {
              return "Điểm: " + context.parsed.y;
            },

            afterBody: function(items) {
              const indexNhom = items[0].dataIndex;
              const muc = items[0].datasetIndex;

              return noiDung[indexNhom][muc];
            }
          }
        }
      }
    }
  });
</script>

</body>
</html>
