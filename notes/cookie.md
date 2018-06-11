## Cookie 運作機制

1. 當使用者透過瀏覽器請求某一個網站時，伺服器可以回應帶有“set-cookie”屬性的Header。
2. 當瀏覽器接收到帶有"set-cookie"的Header時，會自動將cookie的name和value存放到瀏覽器內部的暫存區。
3. 當瀏覽器再次對伺服器發出請求時，就會尋找暫存區內有沒有**該網域**並且**在時效內**的cookie，如果有的話就會加入到這次Request Header中的cookie屬性。