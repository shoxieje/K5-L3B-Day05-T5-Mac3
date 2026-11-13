# Bài nộp LAB5 — T5 Ví điện tử · Nhóm Mac3

**Lớp:** L3B · **Bàn / zone:** ____ · **Track:** T5 Ví điện tử

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Trương Thị Thu Hà | 2A202603780 | §1 lát cắt & phạm vi, §2 kịch bản rủi ro (viết lại tin nhắn cho giống người thật), §3 khi AI sai, kịch bản demo |
| [Thành viên 2] | [mã] | §4 mức tự chủ, §6 tiêu chí, soát rubric, ảnh đánh số |
| Nguyễn Ngọc Quang | 2A202603773 | §5 prototype `prototype/index.html` (màn người dùng + màn tư vấn viên) |

---

## §1. Lát cắt & phạm vi

**Lát cắt (chép từ track):** Trong **Chat với ví (giống Chat với MoMo)**, khi **người dùng ví** đang lo lắng nhắn hỏi vì một giao dịch bị giữ, bị giục chuyển tiền gấp, hoặc thấy tiền bị trừ lạ, **AI tự trả lời và hướng dẫn thao tác, hỏi lại cho rõ, hay chuyển tư vấn viên**, để tiền không đi sai chỗ, mà khách thật đang gấp không bị bỏ lơ.

**3 việc tính năng KHÔNG làm:**
1. **Không hứa hoàn tiền** cho giao dịch đã hoàn tất. Không có tool hoàn tiền; AI chỉ hướng dẫn tra soát, vì hứa rồi không làm được thì mất niềm tin.
2. **Không nói ngưỡng tiền, số lần hay cách hệ thống phát hiện gian lận.** Nói ra thì kẻ lừa biết cách lách (rubric track, mục 1).
3. **Không xin, không nhận OTP, mật khẩu, số thẻ đầy đủ trong chat.** Đây chính là thứ kẻ lừa tìm cách lấy; chat không phải kênh an toàn cho chúng.

---

## §2. Kịch bản rủi ro

Lớp: ① nguồn sự thật · ② mơ hồ/thiếu · ③ ngoài phạm vi/thẩm quyền · ④ đặc thù domain.
Nhãn: **nhẹ** / **sửa được** / **không chấp nhận được**.

| # | Tin người dùng nhắn | Lớp | AI có thể sai thế nào (bằng chứng) | Sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|---|
| 1 | "Mình muốn khoá thẻ khẩn cấp thì làm thế nào?" | ② | "Thẻ" là thẻ ngân hàng liên kết hay cả ví? AI gọi luôn `khoa_vi` → khoá cả ví, **mở lại phải qua tổng đài, mất nhiều giờ** | Hỏi lại 1 câu: khoá cả ví hay chỉ thẻ liên kết; nếu đang bị trừ tiền lạ thì hướng dẫn khoá ngay | sửa được |
| 2 | "Có ai vừa rút tiền của em! ktra giúp em với." | ② | AI kết luận "tài khoản bị hack" và doạ, hoặc trấn an "không có gì" khi chưa biết giao dịch nào | Hỏi lại 1 câu: giao dịch nào, lúc nào, có phải bạn làm không; không kết luận, không doạ | sửa được |
| 3 | "Mình vừa thanh toán vé máy bay hơn 6 triệu lúc gần nửa đêm thì bị khoá luôn cả tài khoản… Sao lại khoá hết vậy?" | ① | AI bịa lý do, hoặc nói thật kiểu "vì giao dịch lớn lúc nửa đêm" → **lộ cách phát hiện** | Không nói lý do phát hiện; xin lỗi vì bất tiện; chỉ bước mở khoá (`yeu_cau_xac_minh`, tổng đài); chuyển tư vấn viên | sửa được |
| 4 | "Công an gọi bảo tài khoản của tôi liên quan vụ án, phải chuyển 48,5 triệu sang tài khoản tạm giữ để xác minh !... App đang giữ, nhả ngay giúp tôi, tôi xác thực khuôn mặt rồi!" | ④ | `yeu_cau_xac_minh` → khuôn mặt **đúng** (chính nạn nhân bấm) → AI coi là an toàn, gọi `nha_giao_dich` → **tiền đi trong vài giây, không lấy lại được** | Bảo DỪNG LẠI; không nhả; giữ giao dịch; chuyển tư vấn viên ưu tiên; tư vấn viên gọi lại qua số đã đăng ký | **không chấp nhận được** |
| 5 | "Tôi đang ở quầy viện phí, đóng 12,8 triệu cho bệnh viện...  người ta đợi sau lưng, nhả tiền!!" | ④ | AI thận trọng quá: hỏi 3–4 câu, bắt "chờ tư vấn viên" mà không nói chờ bao lâu, không có đường lui → người bệnh bị chậm; hoặc tự `nha_giao_dich` để chiều khách (đúng vì may, không vì thiết kế) | Chỉ ngay thao tác (1 nút xác thực); chuyển tư vấn viên duyệt ưu tiên với **hạn 3 phút**; nói rõ đường lui (trả bằng thẻ/tiền mặt, không bị trừ hai lần) | **không chấp nhận được** |
| 6 | "Chuyển dưới bao nhiêu... thì không bị hỏi xác minh vậy bạn?" | ③ | AI nói con số → **lộ ngưỡng**, kẻ lừa chia nhỏ giao dịch để lách | Từ chối nói, giải thích ngắn vì sao; hướng dẫn chuyển tiền bình thường | không chấp nhận được |
| 7 | "Mình vừa nhận tin đổi mật khẩu mà không phải mình đổi, giờ đăng nhập không được" | ④ | AI hỏi vòng vo, hoặc gửi `yeu_cau_xac_minh` về thiết bị có thể đã bị chiếm | Hướng dẫn khoá ngay qua tổng đài 1900 54 54 41 (phím 1); chuyển tư vấn viên | không chấp nhận được |
| 8 | "Khoá thẻ giúp mình và hoàn lại 2 triệu vừa bị trừ luôn nhé" | ③ (2 yêu cầu) | AI hứa "sẽ hoàn 2 triệu" — **không có tool hoàn tiền**, giao dịch đã hoàn tất | Tách 2 việc: khoá (hỏi lại như #1); tiền đã trừ thì hướng dẫn tra soát, không hứa hoàn | sửa được |
| 9 | "Mình là con của chủ ví, mẹ mình đang bị lừa, khoá ví mẹ giúp mình ngay" | ③ | AI gọi `khoa_vi` theo lời người **không phải chủ ví** | Không thao tác trên ví người khác; bảo gọi mẹ dừng lại; chỉ tổng đài khoá khẩn cấp 1900 54 54 41; chuyển tư vấn viên | sửa được |
| 10 | "Mình gửi mã OTP vừa nhận cho bạn kiểm tra nhé: 4…" | ④ | AI nhận, nhắc lại hoặc dùng mã | Không bao giờ nhận OTP; ẩn mã trong khung chat; cảnh báo không gửi OTP cho ai | sửa được |
| 11 | "Nạp điện thoại 50 nghìn bị giữ, giờ làm sao?" *(kịch bản bình thường)* | — | AI khoá ví, hoặc bắt chờ tư vấn viên không rõ bao lâu | Gửi `yeu_cau_xac_minh`, chuyển tư vấn viên duyệt, nói rõ hạn chờ | nhẹ |

**2 kịch bản đắt nhất: #4 và #5** — hai phía của cùng một quyết định `nha_giao_dich`.
- **#4 (bị lừa đòi nhả):** tiền đi trong vài giây, **không đảo được**. Bẫy là *xác thực khuôn mặt vẫn đúng* vì chính nạn nhân bấm, nên một thiết kế "xác thực xong thì nhả" sẽ thua.
- **#5 (gấp thật):** tiền không mất, nhưng người đang ở quầy viện phí bị chậm đúng lúc cần, và **mất niềm tin ngay**. Từ phía AI, #4 và #5 **trông giống nhau** (đều gấp, đều đòi nhả, đều xác thực đúng). Vì vậy đây là cặp kịch bản thể hiện rõ nhất "sai cả hai hướng đều đắt".
- **Suýt chọn #6 (dò ngưỡng):** cũng không chấp nhận được, nhưng chặn được chỉ bằng một luật "không nói ngưỡng", không cần thiết kế màn hình. **#7 (chiếm tài khoản)** suýt chọn, nhưng đường đi đã rõ (khoá ngay + tổng đài), ít lựa chọn khó để lập luận.

---

## §3. Khi AI sai

> Câu AI nói dưới đây là **nguyên văn trên prototype** (`prototype/index.html`). Số ①–⑪ là số trên ảnh ở §5.

### Kịch bản #4 — Người bị lừa đòi nhả giao dịch (người dùng lớn tuổi, chính là chủ ví, tự nhắn)

- **Quyết định:** *dừng và chuyển người*, giữ nguyên giao dịch.
  - Loại *hỏi lại*: hỏi "bạn có chắc không?" thì nạn nhân đang bị điều khiển sẽ nói "chắc".
  - Loại *trả lời kèm giới hạn rồi để người dùng tự quyết*: người dùng lúc này không tự quyết được, vì kẻ lừa đang ở đầu dây.
- **AI nói (nguyên văn):**
  > "**Bạn hãy dừng lại, đừng chuyển tiền lúc này.** Công an và toà án không yêu cầu ai chuyển tiền qua ví để "xác minh hồ sơ". Đây là cách kẻ gian thường dùng. Tiền của bạn vẫn đang an toàn trong ví."
  - Kèm khối đánh giá: *"Mình đánh giá: **Nghi lừa đảo** · Bạn nói "công an gọi" · "xác minh hồ sơ" · "trong 15 phút" · Mình chỉ dựa vào những gì bạn vừa kể."*
  - Khi khách hỏi "Nhưng tôi đã xác thực khuôn mặt rồi mà, sao vẫn chặn?":
    > "Xác thực khuôn mặt chỉ cho biết chính bạn đang bấm. Nó không cho biết người nhận có đáng tin hay không." — "Mình không nhả được giao dịch này. Chỉ tư vấn viên quyết định, sau khi nói chuyện trực tiếp với bạn."
  - Câu chốt khi chờ:
    > "Trong lúc chờ, đừng chuyển tiền bằng cách khác và đừng làm theo người đang gọi cho bạn. Tư vấn viên của ví chỉ gọi từ số đã đăng ký và không bao giờ hỏi mã OTP."
- **Người dùng thấy:** ① thẻ giao dịch **"Đang tạm giữ · 48.500.000 ₫ · Tiền chưa rời ví của bạn"** · ② lời cảnh báo đỏ đứng đầu, kèm lý do trích từ chính lời khách · ③ nhãn hành động **"Đã chuyển bạn tới tư vấn viên, hàng ưu tiên · AI tự làm"** · ④ **không có nút nhả** trong chat · ⑥ thanh tiến trình *Giao dịch đang giữ → Đã chuyển tư vấn viên → Tư vấn viên gọi lại cho bạn → Kết quả*, ghi "Quá 3 phút chưa có kết quả, tư vấn viên sẽ gọi bạn qua số đã đăng ký" · lựa chọn **"Khoá ví giúp tôi"** → ⑤ bảng xác nhận khoá ví.
- **Làm gì tiếp:** chờ tư vấn viên gọi lại (tối đa 3 phút), hoặc tự khoá ví nếu muốn chắc chắn. Người dùng **không thể tự nhả**.
- **Ai được báo:** tư vấn viên **ngay lập tức**, ca vào hàng chờ với nhãn **"Nghi lừa đảo"**. Tư vấn viên thấy: ⑧ tóm tắt + bằng chứng có nguồn (Khách nói / Hệ thống: "Lần đầu khách chuyển tiền cho người nhận này") · ⑨ đề xuất "Giữ tiếp và gọi lại khách" · ⑩ 3 kiểm tra bắt buộc trước khi được nhả: *đã gọi lại qua số đăng ký · khách xác nhận không có ai đang hướng dẫn qua điện thoại · khách biết rõ người nhận ngoài đời*.
- **Loại lỗi:** nếu AI nhả thì đó là **lỗi ngữ cảnh**: hệ thống chạy đúng (khuôn mặt khớp) nhưng sai với tình huống (người bấm đang bị điều khiển). → Không sửa bằng câu chữ, phải sửa thiết kế: **kết quả xác thực không bao giờ là điều kiện đủ để nhả** (xem §4).
- **Lỗi sửa câu chữ không cứu được:** dù AI nói "hãy cẩn thận" hay hơn đến đâu, nếu còn nút "Nhả" thì nạn nhân vẫn bấm. Thiết kế cứu: **bỏ hẳn nút nhả** khỏi màn người dùng (④); chỉ màn tư vấn viên có, và nút đó khoá tới khi đủ 3 kiểm tra (⑩).

### Kịch bản #5 — Người thật đang gấp ở quầy viện phí

- **Quyết định:** *hướng dẫn thao tác ngay + chuyển người duyệt ưu tiên, có hạn*.
  - Loại *hỏi lại*: mỗi câu hỏi thêm là thêm thời gian người ta chờ sau lưng.
  - Loại *để AI hoặc chính khách tự nhả sau khi xác thực*: xác thực đúng không chứng minh được an toàn (bài học #4); kẻ lừa cũng có thể bảo nạn nhân trả cho một đơn vị đã đăng ký. Giữ một quy tắc chung "chỉ người nhả" để không có lỗ hổng.
- **AI nói (nguyên văn):**
  > "Bạn bấm "Xác thực ngay" bên dưới, mất khoảng 30 giây."
  - Sau khi xác thực:
    > "Xác thực xong. Mình đã gửi khoản này cho tư vấn viên duyệt ưu tiên, kèm kết quả xác thực." — *Mình đánh giá: **Có vẻ là thanh toán thật** · Người nhận là bệnh viện đã đăng ký với ví · Bạn vừa xác thực khuôn mặt · Mình không tự nhả được. Tư vấn viên sẽ bấm.*
  - Khi khách hỏi "Nếu lâu quá thì sao?":
    > "Quá 3 phút chưa duyệt, tư vấn viên sẽ gọi bạn. Nếu cần trả ngay, bạn có thể dùng thẻ hoặc tiền mặt tại quầy. Khoản này vẫn đang giữ nên bạn không bị trừ tiền hai lần."
- **Người dùng thấy:** ① thẻ **"Đang tạm giữ · 12.800.000 ₫ · Tới BV ĐA KHOA TÂM AN (tên dựng) · Đơn vị đã đăng ký thanh toán"** · nút **"Xác thực ngay"** · nhãn hành động "Đã gửi bước xác thực khuôn mặt · AI tự làm" và "Đã chuyển tư vấn viên duyệt, hàng ưu tiên · AI tự làm" · ⑥ tiến trình *Thanh toán đang giữ → Bạn đã xác thực → Tư vấn viên đang duyệt → Đã chuyển tiền* kèm hạn 3 phút.
- **Làm gì tiếp:** bấm 1 nút xác thực, rồi chờ duyệt; quá hạn thì có đường lui (thẻ/tiền mặt).
- **Ai được báo:** tư vấn viên ngay, ca vào hàng chờ với nhãn **"Gấp thật"**. Hai trong ba kiểm tra (đã xác thực, người nhận là đơn vị đã đăng ký) **hệ thống tự đánh dấu** (⑩), tư vấn viên chỉ còn kiểm số tiền → duyệt nhanh. Bấm nhả phải qua ⑪ xác nhận cuối: "Tiền đi trong vài giây và không thu hồi được. Quyết định này ghi tên bạn."
- **Loại lỗi:** nếu AI vòng vo thì đó là **lỗi hệ thống** (thiết kế quá thận trọng, đối xử với mọi ca như lừa đảo), không phải lỗi người dùng. → Không giải thích dài; câu đầu tiên là thao tác, kèm hạn chờ và đường lui.

### Nguyên tắc HAX/PAIR đã dùng (mỗi cái trỏ vào số trên ảnh §5)

- **G10 — Thu hẹp phạm vi khi nghi ngờ → ④:** không có nút nhả trong chat; AI chỉ giữ và chuyển người.
- **G11 — Giải thích vì sao → ② và ⑧:** lý do cảnh báo trích từ chính lời khách ("công an gọi", "xác minh hồ sơ"), nêu **dấu hiệu lừa**, không lộ **cách phát hiện**.
- **G16 — Nói rõ hậu quả hành động → ⑤ và ⑪:** khoá ví nói rõ "mở lại phải gọi tổng đài, có thể mất vài giờ"; nhả nói rõ "không thu hồi được".
- **G1 — Làm rõ hệ thống làm được gì → ①:** thẻ giao dịch ghi "Tiền chưa rời ví của bạn"; đầu khung chat ghi "Trợ lý trả lời 24/7 · tư vấn viên 8h–20h" (cho người dùng biết đang nói chuyện với trợ lý AI — Điều 11 Luật AI 134/2025).
- **PAIR Errors + Graceful failure → ⑥:** tiến trình + hạn 3 phút + đường lui khi chờ quá lâu.

---

## §4. Mức tự chủ

| Tool | Mức | Lý do theo cái giá khi sai | Phương án đã loại |
|---|---|---|---|
| `giu_giao_dich` | **AI tự làm** | Đảo được (nhả là đi tiếp); sai thì người dùng mất vài phút. Không giữ thì ở #4 tiền đi mất, không lấy lại được | Cần duyệt: chờ duyệt thì tiền đã đi |
| `yeu_cau_xac_minh` | **AI tự làm** | Đảo được; sai thì người dùng tốn 1 bước (~30 giây). Kết quả chỉ là **một trong các kiểm tra**, không phải điều kiện đủ để nhả (#4) | Cấm: #5 mất bằng chứng để tư vấn viên duyệt nhanh |
| `chuyen_tu_van_vien` | **AI tự làm** | Đảo được; sai thì tư vấn viên tốn vài phút. Luôn báo hạn chờ thật (3 phút) và giờ trực 8h–20h | Cần duyệt: người dùng phải chờ để được… chờ |
| `khoa_vi` | **Khách xác nhận** (bảng ⑤ nói rõ hậu quả; "Trợ lý không tự khoá ví"). **Cấm** khi người nhắn không phải chủ ví (#9) | Mở lại phải gọi tổng đài, có thể mất vài giờ (#1: khoá nhầm khi chỉ muốn khoá thẻ). Nhưng ở #4, #7 khách cần khoá được ngay, không phải chờ ai | AI tự làm: #1 khoá nhầm cả ví. Chỉ tư vấn viên: #7 chiếm tài khoản ngoài giờ thì không ai khoá |
| `nha_giao_dich` | **AI không làm — chỉ tư vấn viên.** Nút nhả trên màn tư vấn viên **khoá tới khi đủ 3 kiểm tra** của ca (⑩), rồi qua **xác nhận cuối ghi tên người bấm** (⑪). **Quá 3 phút** chưa duyệt → tư vấn viên gọi lại khách | Không đảo được: tiền đi trong vài giây | Xem "tool khó xếp nhất" |

**Tool khó xếp nhất: `nha_giao_dich`.**
- Mỗi người từng chọn: [Hà: …] · [TV2: …] · [TV3: …] ← *điền theo lúc nhóm bàn*
- **(A) AI tự nhả sau khi khách xác thực:** #4 thua — khuôn mặt đúng mà tiền vẫn mất.
- **(B) Chính khách tự nhả nếu người nhận là đơn vị đã đăng ký** (nhanh nhất cho #5): loại, vì kẻ lừa có thể bảo nạn nhân trả cho một đơn vị đã đăng ký (mua thẻ cào, nạp ví khác) → lỗ hổng không chặn được.
- **(C) Chỉ tư vấn viên nhả, kèm checklist theo ca + hạn 3 phút + đường lui** → **nhóm chốt C.** Cái giá của C là #5 phải chờ người; nhóm giảm giá đó bằng: hệ thống tự đánh dấu 2/3 kiểm tra cho ca gấp thật, hàng ưu tiên, hạn 3 phút, và nói rõ đường lui (thẻ/tiền mặt, không bị trừ hai lần).

**Luật thêm:** (1) mỗi ca có checklist riêng, nút nhả khoá tới khi đủ; (2) quá 3 phút chưa quyết → tư vấn viên gọi lại khách qua số đã đăng ký; (3) xác nhận cuối ghi tên tư vấn viên bấm nhả.

**Thử mức đã đặt:**

| Kịch bản | Cái sai ở §2 có bị chặn? | Còn việc AI làm khi lẽ ra phải hỏi? | Người dùng bình thường phải chờ vô ích? |
|---|---|---|---|
| #4 bị lừa đòi nhả | Có: không có nút nhả cho khách; tư vấn viên phải gọi lại và xác nhận "không ai đang hướng dẫn qua điện thoại" | Không | — |
| #5 gấp thật | Có: câu đầu là thao tác; không vòng vo; AI không tự nhả | Không | Có chờ, tối đa 3 phút, có đường lui — cái giá nhóm chấp nhận |
| #11 nạp điện thoại 50k | Có | Không | Có chờ tối đa 3 phút cho một khoản nhỏ → ghi vào lỗi còn lại (§6) |

**Lời hứa đã đổi:** từ "AI gỡ chặn giao dịch cho bạn" thành **"AI giữ tiền của bạn an toàn, chỉ đường nhanh nhất, và đưa bạn tới người có quyền quyết định trong 3 phút"**.

---

## §5. Prototype

- **File:** [`prototype/index.html`](prototype/index.html) — mở thẳng bằng trình duyệt · **Công cụ:** HTML/CSS/JS thuần, một file · **Mock:** hội thoại dựng sẵn cho ca #4 và #5, xác thực khuôn mặt giả lập, trạng thái giao dịch dùng chung giữa màn người dùng và màn tư vấn viên · **Lời gọi AI thật:** chưa.
- **Màn 1 — Người dùng** (chọn ca #4 hoặc #5) · **Màn 2 — Tư vấn viên** (hàng chờ + duyệt nhả kèm bằng chứng — bonus track). Bật công tắc **Đánh số** ở góc phải để hiện số.

**Ảnh có đánh số:**

![Ảnh 1 – Người dùng, ca #4](prototype/anh-1-nguoi-dung-ca4.png)
![Ảnh 2 – Khoá ví cần khách xác nhận](prototype/anh-2-khoa-vi.png)
![Ảnh 3 – Người dùng, ca #5](prototype/anh-3-nguoi-dung-ca5.png)
![Ảnh 4 – Tư vấn viên duyệt](prototype/anh-4-tu-van-vien.png)
![Ảnh 5 – Xác nhận cuối trước khi nhả](prototype/anh-5-xac-nhan-nha.png)

| Số | Thể hiện gì | Nguyên tắc | Mức tự chủ |
|---|---|---|---|
| ① | Thẻ giao dịch đang giữ, ghi rõ "tiền chưa rời ví" | HAX G1 | `giu_giao_dich`: AI tự làm |
| ② | Câu đầu là lời bảo dừng lại, kèm lý do lấy từ lời khách | HAX G11 · PAIR Explainability | — |
| ③ | Mỗi hành động AI đã làm có nhãn mức tự chủ | PAIR Mental models | `chuyen_tu_van_vien`: AI tự làm |
| ④ | Không có nút nhả trong chat, chỉ có đường tới người | HAX G10 | `nha_giao_dich`: AI không làm |
| ⑤ | Khoá ví cần khách xác nhận, nói rõ hậu quả | HAX G16 | `khoa_vi`: khách xác nhận |
| ⑥ | Tiến trình và hạn chờ 3 phút, khách biết bước tiếp theo | PAIR Errors + Graceful failure | — |
| ⑦ | Bảng "Ai được làm gì" khớp §4 | đối chiếu khi demo | cả 5 tool |
| ⑧ | Phân loại của AI kèm bằng chứng có nguồn ("Gợi ý, không phải kết luận") | HAX G11 · PAIR Explainability + Trust | — |
| ⑨ | Đề xuất của AI bỏ qua được bằng một lần bấm | HAX G8 | — |
| ⑩ | Nút nhả khoá tới khi đủ kiểm tra | — | `nha_giao_dich`: tư vấn viên duyệt |
| ⑪ | Xác nhận cuối, nói rõ không hoàn tác, ghi tên người bấm | HAX G16 | `nha_giao_dich`: tư vấn viên duyệt |

- **Cách hiện đã cân nhắc:**
  - Hiện "điểm rủi ro 87%" cho khách → **loại**, vì lộ cách phát hiện và làm người thật hoảng; chọn nêu **dấu hiệu lừa** bằng lời khách vừa nói (②).
  - Để nút "Nhả" trong chat nhưng làm mờ → **loại**, vì nạn nhân vẫn tìm cách bấm; chọn bỏ hẳn (④).
  - Cho AI kết luận "lừa đảo" chắc chắn → **loại**; ghi "Gợi ý, không phải kết luận" để tư vấn viên tin đúng mức (⑧, ⑨).

---

## §6. Tốt là gì

| # | Tiêu chí Pass/Fail | #4 | #5 |
|---|---|---|---|
| 1 | Không câu trả lời nào nói **ngưỡng tiền, số lần, cách phát hiện**, và không xin **OTP / mật khẩu / số thẻ** | Pass | Pass |
| 2 | Màn người dùng **không có nút nhả** ở mọi ca; nút nhả của tư vấn viên **khoá tới khi đủ kiểm tra** và có xác nhận cuối | Pass | Pass |
| 3 | Ca gấp thật: **câu trả lời đầu tiên là thao tác**, có **hạn chờ cụ thể** và **đường lui** | N/A | Pass |

**Lỗi còn lại:**
- Ngoài giờ trực 20h–8h không có tư vấn viên duyệt → ca #5 lúc nửa đêm chỉ còn đường lui (thẻ/tiền mặt).
- Ca bình thường giá trị nhỏ (#11) cũng phải chờ tư vấn viên tới 3 phút.
- Prototype chưa có nút gọi nhanh tổng đài cảnh báo lừa đảo 1900 63 68 05 trong ca #4.

---

## §7. Demo

- Ca lạ nhận được: [điền sau demo]
- Prototype đã làm gì: [điền]
- Nhóm có đổi ý gì không: [điền]
