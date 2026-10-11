# bieu do tuong tac
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 10px;
      background: white;
    }

    .chart-container {
      position: relative;
      width: 100%;
      height: 350px;
    }
  </style>
</head>

<body>

<div class="chart-container">
  <canvas id="myChart"></canvas>
</div>

<script>
  // TÊN CỦA 3 CỘT: BẠN TỰ SỬA
  const tenCot = [
    "Mức 1",
    "Mức 2",
    "Mức 3"
  ];

  // GIÁ TRỊ CỦA 3 CỘT: BẠN TỰ SỬA
  const giaTri = [1, 2, 3];

  // NỘI DUNG HIỆN RA KHI DI CHUỘT: BẠN TỰ SỬA
  const noiDung = [
    "Bạn tự nhập nội dung cho mức 1 tại đây.",
    "Bạn tự nhập nội dung cho mức 2 tại đây.",
    "Bạn tự nhập nội dung cho mức 3 tại đây."
  ];

  new Chart(document.getElementById("myChart"), {
    type: "bar",

    data: {
      labels: tenCot,

      datasets: [{
        label: "Giá trị",
        data: giaTri,

        backgroundColor: [
          "#174F79",
          "#174F79",
          "#174F79"
        ],

        hoverBackgroundColor: "#327BA9",

        barPercentage: 0.65,
        categoryPercentage: 0.8
      }]
    },

    options: {
      responsive: true,
      maintainAspectRatio: false,

      plugins: {
        legend: {
          display: false
        },

        tooltip: {
          displayColors: false,

          callbacks: {
            title: function(items) {
              return tenCot[items[0].dataIndex];
            },

            label: function(context) {
              return "Giá trị: " + context.parsed.y;
            },

            afterBody: function(items) {
              return noiDung[items[0].dataIndex];
            }
          }
        }
      },

      scales: {
        x: {
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
            text: "Mức điểm"
          }
        }
      }
    }
  });
</script>

</body>
</html>
