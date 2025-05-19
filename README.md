📦JavaWebOrder
      └── 📁 src/main/java
                 ├── 📁 controller
                 │       └── ☕ OrderServlet.java         ← 控制層（Controller）
                 ├── 📁 service
                 │       └── ☕ OrderService.java         ← 商業邏輯層（Service）
                 ├── 📁 dao
                 │       └──☕  OrderDAO.java              ← 資料存取層（DAO）
                 └── 📁 model
                           ├── 📁 entity
                           │        └── ☕ Order.java            ← 資料庫對應物件（Entity）
                           └── 📁 dto
                                      └── ☕ OrderDTO.java    ← 對外傳輸物件（DTO）
 └── 📁 src
         └──📁 main
                  └── 📁 webapp
                            │    └── 📝 index.jsp                   ← 首頁/點餐頁
                            └──📁  WEB-INF
                                     ├── 📝 result.jsp                ← 點餐結果頁
                                     └── 📝 history.jsp              ← 歷史訂單查詢


[ index.jsp ]
   ↓ (POST)
[ OrderServlet.doPost ]
   ↓ 呼叫
[ OrderService.placeOrder ]
   ↓ 建立 Entity + 存 DAO + 回傳 DTO
[ result.jsp 顯示 DTO 資料 ]

用戶點擊「查看歷史訂單」
   ↓ (GET)
[ OrderServlet.doGet ]
   ↓ 呼叫
[ OrderService.getOrderHistory ]
   ↓ 回傳 List<OrderDTO>
[ history.jsp 顯示列表 ]


進入首頁 index.jsp
顯示下拉選單：牛肉麵、陽春麵
使用者選擇一項 → 點【送出訂單】


進入 Controller：OrderServlet.doPost()
接收表單資料 item
呼叫 Service：OrderService.placeOrder(item)


Service 商業邏輯
判斷餐點對應價格（例如：牛肉麵 → 120 元）
建立 Order 實體，存入 DAO
回傳 OrderDTO 給前端


結果頁面 result.jsp
顯示點餐結果：「你點了牛肉麵，價格 120 元」


查看歷史訂單（GET 請求）
使用者點「查看歷史訂單」連結
OrderServlet.doGet() 呼叫 OrderService.getOrderHistory()
將所有歷史 OrderDTO 傳給 history.jsp
顯示所有曾點的餐點與價格
