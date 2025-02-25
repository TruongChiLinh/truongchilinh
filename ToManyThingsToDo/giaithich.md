jq : dùng phân tích file json (./transaction-log.txt)
select(.symbol == "TSLA") lọc ra các giao dịch có symbol là TSLA
.orther_id lấy orther_id của transaction
-r lấy giá trị ko lấy dấu ngặc kép

xargs lấy từng orther_id đã làm jq -r '. | select(.symbol == "TSLA") | .order_id' ./transaction-log.txt thay vào {} trong lệnh curl

curl -s gửi yêu cầu HTTP GET đến https://example.com/api/{orther_id}, trong đó {orther_id}
được thay thế bằng giá trị orther_id thực tết đã lọc ra
>> ./output.txt:
lệnh này sẽ ghi kết quả của từng yêu cầu curl vào cuối tệp ./output.txt.

kết quả là sau khi gửi xong yêu cầu GET cho mỗi orther_id có symbol là TSLA 
những phản hồi này sẽ được ghi vào log