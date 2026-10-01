# Day 14 — Reflection

## Evaluation Report & Failure Analysis

Dùng kết quả thật trong `artifacts/benchmark_results.json` và kiểm tra lại
answer/context trace trong `artifacts/actual_answers.json` trước khi kết luận.

> **Trạng thái offline:** Golden dataset đã được hoàn thiện và validator báo
> PASS. Chưa chạy DomainAssistant vì CP4 cần OpenAI API và key trước đó đã bị
> lộ; không tạo số liệu benchmark hoặc failure cases giả. Các mục cần score,
> trace và 5 Whys phải được hoàn tất sau khi chạy benchmark bằng key mới.

---

## 1. Benchmark Results Summary

**Overall pass rate:** N/A — chưa có `benchmark_results.json`.

| Metric | Average | Min | Max | Nhận xét |
|---|---:|---:|---:|---|
| Context Recall | N/A | N/A | N/A | Chưa chạy benchmark thật. |
| Context Precision | N/A | N/A | N/A | Chưa chạy benchmark thật. |
| Faithfulness | N/A | N/A | N/A | Chưa có actual answers để chấm. |
| Relevance | N/A | N/A | N/A | Chưa có actual answers để chấm. |
| Completeness | N/A | N/A | N/A | Chưa có actual answers để chấm. |
| Overall Score | N/A | N/A | N/A | Chưa có actual answers để chấm. |

**Score interpretation**

- Metrics/cases ở mức Good (0.8–1.0): Chưa xác định — chưa có scores thực.
- Metrics/cases ở mức Needs Work (0.6–0.8): Chưa xác định — chưa có scores thực.
- Metrics/cases ở mức Significant Issues (<0.6): Chưa xác định — chưa có scores thực.

**Failure type distribution**

| Failure Type | Count | Percentage |
|---|---:|---:|
| hallucination | N/A | N/A |
| irrelevant | N/A | N/A |
| incomplete | N/A | N/A |
| off_topic | N/A | N/A |
| refusal | N/A | N/A |

**Chẩn đoán tổng quan:** Vấn đề chính nằm ở retrieval, generation hay cả hai?
Dùng ít nhất hai metrics để bảo vệ kết luận.

> Chưa thể xác định retrieval, generation hay cả hai là vấn đề chính nếu chưa
> có trace và scores. Sau khi chạy, so sánh Context Recall/Precision với
> Faithfulness/Completeness: retrieval thấp cùng answer score thấp gợi ý thiếu
> hoặc xếp hạng sai evidence; retrieval tốt nhưng answer score thấp gợi ý lỗi
> generation/prompt. Hiện chưa có dữ liệu để chọn kết luận.

---

## 2. Top 3 Worst Failures — 5 Whys

Phân loại failure trước khi đề xuất fix. Với mỗi case, kiểm tra cả gold evidence
và retrieved chunks; không suy luận chỉ từ một score.

### Failure 1

**ID và question:**

> N/A — chưa có benchmark artifact để xác định Failure 1.

**Expected answer:**

> N/A — expected answers có trong golden dataset nhưng chưa chọn được failure thực.

**Actual answer:**

> N/A — DomainAssistant chưa chạy; không có actual answer trace.

**Scores:** Context Recall: N/A | Context Precision: N/A | Faithfulness: N/A |
Relevance: N/A | Completeness: N/A | Overall: N/A — benchmark chưa chạy.

**Evidence inspection:** Retriever lấy đúng/thiếu/thừa chunks nào?

> Chưa có retrieved-context trace để xác định chunk đúng, thiếu hoặc thừa.

| Level | Question | Answer |
|---|---|---|
| Symptom | Vấn đề quan sát được là gì? | Chưa có failure thực tế được benchmark ghi nhận. |
| Why 1 | Tại sao symptom xảy ra? | Chưa xác định; cần actual answer và scores. |
| Why 2 | Tại sao nguyên nhân trên xảy ra? | Chưa xác định; cần kiểm tra retrieved chunks. |
| Why 3 | Tại sao vấn đề đó chưa được ngăn chặn? | Chưa xác định; chưa có failure cụ thể để truy nguyên. |
| Why 4 | Tại sao cơ chế hiện tại chưa phát hiện hoặc xử lý được? | Chưa xác định; cần đối chiếu trace với prompt và guardrails. |
| Why 5 | Root cause có thể hành động được là gì? | Chưa thể kết luận nếu chưa kiểm chứng nguyên nhân bằng evidence. |

**Root cause từ `find_root_cause()`:**

> N/A — chưa có EvalResult của failure để gọi `find_root_cause()`.

**Bạn đồng ý hay không? Dẫn evidence từ trace:**

> Chưa thể đồng ý hoặc phản biện root cause khi chưa có output và trace tương ứng.

**Proposed fix cụ thể:**

> Sau khi có trace, sửa nguyên nhân được evidence xác nhận (retrieval, prompt,
> generation hoặc safety guardrail), thêm case tái hiện vào golden set và đo
> lại metric liên quan. Chưa chọn fix riêng cho một failure chưa quan sát.

### Failure 2

**ID và question:**

> N/A — chưa có benchmark artifact để xác định Failure 2.

**Expected answer:**

> N/A — expected answers có trong golden dataset nhưng chưa chọn được failure thực.

**Actual answer:**

> N/A — DomainAssistant chưa chạy; không có actual answer trace.

**Scores:** Context Recall: N/A | Context Precision: N/A | Faithfulness: N/A |
Relevance: N/A | Completeness: N/A | Overall: N/A — benchmark chưa chạy.

**Evidence inspection:**

> Chưa có retrieved-context trace để xác định chunk đúng, thiếu hoặc thừa.

| Level | Question | Answer |
|---|---|---|
| Symptom | Vấn đề quan sát được là gì? | Chưa có failure thực tế được benchmark ghi nhận. |
| Why 1 | Tại sao symptom xảy ra? | Chưa xác định; cần actual answer và scores. |
| Why 2 | Tại sao nguyên nhân trên xảy ra? | Chưa xác định; cần kiểm tra retrieved chunks. |
| Why 3 | Tại sao vấn đề đó chưa được ngăn chặn? | Chưa xác định; cần failure cụ thể để truy nguyên. |
| Why 4 | Tại sao cơ chế hiện tại chưa phát hiện hoặc xử lý được? | Chưa xác định; cần đối chiếu trace với prompt và guardrails. |
| Why 5 | Root cause có thể hành động được là gì? | Chưa thể kết luận nếu chưa kiểm chứng nguyên nhân bằng evidence. |

**Root cause và proposed fix:**

> N/A — chưa có failure thực để xác định root cause hoặc đề xuất fix dựa trên trace.

### Failure 3

**ID và question:**

> N/A — chưa có benchmark artifact để xác định Failure 3.

**Expected answer:**

> N/A — expected answers có trong golden dataset nhưng chưa chọn được failure thực.

**Actual answer:**

> N/A — DomainAssistant chưa chạy; không có actual answer trace.

**Scores:** Context Recall: N/A | Context Precision: N/A | Faithfulness: N/A |
Relevance: N/A | Completeness: N/A | Overall: N/A — benchmark chưa chạy.

**Evidence inspection:**

> Chưa có retrieved-context trace để xác định chunk đúng, thiếu hoặc thừa.

| Level | Question | Answer |
|---|---|---|
| Symptom | Vấn đề quan sát được là gì? | Chưa có failure thực tế được benchmark ghi nhận. |
| Why 1 | Tại sao symptom xảy ra? | Chưa xác định; cần actual answer và scores. |
| Why 2 | Tại sao nguyên nhân trên xảy ra? | Chưa xác định; cần kiểm tra retrieved chunks. |
| Why 3 | Tại sao vấn đề đó chưa được ngăn chặn? | Chưa xác định; cần failure cụ thể để truy nguyên. |
| Why 4 | Tại sao cơ chế hiện tại chưa phát hiện hoặc xử lý được? | Chưa xác định; cần đối chiếu trace với prompt và guardrails. |
| Why 5 | Root cause có thể hành động được là gì? | Chưa thể kết luận nếu chưa kiểm chứng nguyên nhân bằng evidence. |

**Root cause và proposed fix:**

> N/A — chưa có failure thực để xác định root cause hoặc đề xuất fix dựa trên trace.

---

## 3. Failure Clustering

Một root cause có thể tạo ra nhiều failures. Nhóm theo nguyên nhân có thể sửa,
không chỉ nhóm theo tên metric.

| Cluster | Root Cause | Failure IDs | Priority |
|---|---|---|---|
| 1 | Chưa phân cụm — chưa có failure và retrieved-context trace. | N/A | Chưa xếp hạng |
| 2 | Chưa phân cụm — chưa có failure và retrieved-context trace. | N/A | Chưa xếp hạng |
| 3 | Chưa phân cụm — chưa có failure và retrieved-context trace. | N/A | Chưa xếp hạng |

**Nếu chỉ được sửa một cluster, bạn chọn cluster nào và vì sao?**

> Chưa thể ưu tiên cluster trước khi có failure quan sát được. Sau khi benchmark,
> chọn nguyên nhân gốc có evidence rõ, ảnh hưởng nhiều case và rủi ro cao nhất.

---

## 4. Improvement Log

Paste output của `generate_improvement_log()`:

```text
Chưa có failure thực để truyền vào generate_improvement_log(); chưa thể đưa
output thực của hàm vào đây.
```

**Ba improvement suggestions ưu tiên**

1. Candidate trước benchmark: kiểm tra retrieval cho câu hỏi policy có nhiều điều kiện hoặc phụ thuộc ngày hiệu lực.
2. Candidate trước benchmark: yêu cầu câu trả lời bảo toàn điều kiện, ngoại lệ và căn cứ evidence.
3. Candidate trước benchmark: mở rộng kiểm thử prompt injection, privacy và an toàn thiết bị.

Với mỗi suggestion, nêu metric dự kiến thay đổi và cách đo lại.

| Suggestion | Target metric | Verification method |
|---|---|---|
| Kiểm tra retrieval cho policy nhiều điều kiện/ngày hiệu lực. | Context Recall, Context Precision | Đối chiếu chunks với gold evidence trên cùng các QA policy trước/sau thay đổi retriever. |
| Bảo toàn điều kiện, ngoại lệ và evidence trong câu trả lời. | Faithfulness, Completeness | Chạy lại golden set; kiểm tra claim và từng ý bắt buộc so với evidence/reference. |
| Thêm kiểm thử injection, privacy và an toàn thiết bị. | Faithfulness; safety review | Chạy regression cases adversarial và xác nhận không tiết lộ dữ liệu hay đưa hướng dẫn nguy hiểm. |

---

## 5. Regression Testing Strategy

**Câu 1: Khi nào chạy `run_regression()` trong production workflow?**

> Chạy trên cùng golden set sau mọi thay đổi code, prompt, model hoặc retriever
> và trước khi deploy; lưu baseline theo phiên bản để so sánh. Chạy lại khi
> phát hành model/prompt mới và trong CI để chặn thay đổi gây suy giảm vượt
> ngưỡng. Không so sánh hai run dùng dataset hoặc policy version khác nhau nếu
> chưa chuẩn hóa chúng.

**Câu 2: Threshold drop 0.05 có phù hợp OrbitTech Customer Support không? Vì sao?**

> 0.05 là ngưỡng khởi điểm dễ hiểu cho regression nhưng không nên là tiêu chí
> duy nhất. Với claim về thanh toán, bảo mật, chính sách hoặc an toàn thiết bị,
> một lỗi nghiêm trọng phải block dù trung bình toàn tập chỉ giảm ít. Cần hiệu
> chỉnh ngưỡng theo baseline ổn định, cỡ mẫu và mức độ rủi ro; theo dõi riêng
> các nhóm câu hỏi quan trọng để tránh average che khuất regression.

**Câu 3: Metric/failure nào phải block deployment, metric nào chỉ alert?**

> Block nếu có rò rỉ dữ liệu, làm theo prompt injection, hướng dẫn không an
> toàn, bịa chính sách/quyền lợi trọng yếu hoặc regression vượt ngưỡng ở
> faithfulness/correctness trên nhóm high-risk. Context Recall/Precision thấp
> nên alert hoặc block khi vượt ngưỡng đã hiệu chỉnh trên case quan trọng.
> Relevance/completeness giảm nhẹ có thể cảnh báo và yêu cầu review, nhưng lỗi
> làm khách thực hiện sai giao dịch hoặc bỏ lỡ quyền lợi phải block.

**Câu 4: Điền evaluation stages vào flow.**

```text
Code/prompt/retrieval change → [Unit tests] → [Golden-set evaluation] → [Regression + safety gate] → Deploy
```

> Chạy kiểm tra deterministic trước; sau đó đánh giá trên cùng golden set,
> kiểm tra failure/high-risk cases và so với baseline. Chỉ deploy khi required
> tests pass và không có safety blocker hoặc regression vượt ngưỡng.

---

## 6. Continuous Improvement Loop

```text
Evaluate → Analyze → Improve → Augment benchmark → Repeat
```

| Priority | Action | Metric dự kiến cải thiện | Expected impact |
|---:|---|---|---|
| 1 | Bổ sung/kiểm tra query và gold evidence cho các policy có ngày hiệu lực, rồi cải thiện retrieval trên nhóm đó. | Context Recall, Context Precision | Ít bỏ sót policy version và ít nhầm lẫn giữa các điều kiện. |
| 2 | Bắt buộc câu trả lời nêu điều kiện, ngoại lệ và nguồn evidence; kiểm tra claim không được hỗ trợ. | Faithfulness, Completeness | Giảm câu trả lời thiếu điều kiện hoặc khẳng định quá mức. |
| 3 | Thêm test adversarial về prompt injection, dữ liệu riêng tư và thiết bị nguy hiểm; yêu cầu từ chối an toàn nhưng vẫn trả lời phần hợp lệ. | Faithfulness, Relevance; safety review | Bắt lỗi ranh giới an toàn trước deployment. |

**Hai hoặc ba failure cases nào cần thêm vào benchmark ở vòng tiếp theo?**

> Sau khi xem trace thật, bổ sung các biến thể tối thiểu cho: (1) câu hỏi về
> return policy trước/sau ngày hiệu lực có và không có OrbitPlus; (2) retrieved
> chunk chứa chỉ dẫn injection cạnh câu hỏi support hợp lệ; (3) lẫn giữa
> shipping delay, carrier trace và damage được báo trong 48 giờ. Không thêm lại
> các case trùng ý; mỗi case mới cần evidence chính xác và expected answer
> được review.

---

## 7. Final Reflection

**Điều gì trong kết quả benchmark trái với dự đoán ban đầu của bạn?**

> Chưa thể kết luận trước khi có actual answers và benchmark artifacts. Hoàn tất
> câu trả lời này sau lần chạy thật bằng cách nêu một quan sát cụ thể cùng ID,
> score và evidence trace; không suy đoán thay cho kết quả.

**Word-overlap heuristics trong lab có giới hạn gì? Nếu đưa hệ thống vào
production, bạn sẽ thay hoặc bổ sung metric nào?**

> Word overlap không hiểu paraphrase/synonym, phủ định, quan hệ ngữ nghĩa hay
> tính đúng sai theo ngữ cảnh; nó cũng có thể thưởng một câu có từ khóa đúng
> nhưng sai quan hệ. Production nên kết hợp retrieval metrics với semantic
> answer metrics và groundedness/citation checks, hiệu chỉnh LLM-as-a-Judge
> trên nhãn human-reviewed, đồng thời giữ safety-specific tests và human review
> cho payment, privacy, policy-version và thiết bị nguy hiểm. Các automated
> scores cần được theo dõi cùng false-positive/false-negative trên bộ kiểm
> định độc lập.
