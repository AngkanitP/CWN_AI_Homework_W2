# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: part2.spec.ts >> TC-PDPA-02 API (JSON) ไม่ส่งเลขบัตรเต็ม
- Location: tests\part2.spec.ts:820:1

# Error details

```
Error: off.reg1 GET /api/officer/queue?filter=all ไม่มีเลข 13 หลัก

expect(received).not.toMatch(expected)

Expected pattern: not /\d{13}/
Received string:      "{\"items\":[{\"caseNo\":\"EG-2569-000020\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-11-30T16:30:00+07:00\",\"slaLevel\":\"overdue\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000022\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-01T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000024\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-02T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000023\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000025\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000026\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000013\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000015\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000027\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000028\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000029\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000030\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000016\",\"serviceId\":\"SV-02\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-08T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000018\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000019\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"APPROVED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000012\",\"serviceId\":\"SV-03\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":1,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000021\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"}],\"filter\":\"all\",\"workload\":3}"
```

```
Error: off.reg1 GET /api/officer/queue?filter=all ไม่มี key idNo

expect(received).not.toContain(expected) // indexOf

Expected value: not "idNo"
Received array:     ["items", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "filter", "workload"]
```

```
Error: off.reg1 GET /api/officer/queue?filter=all ไม่มี 3100600987659

expect(received).not.toContain(expected) // indexOf

Expected substring: not "3100600987659"
Received string:        "{\"items\":[{\"caseNo\":\"EG-2569-000020\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-11-30T16:30:00+07:00\",\"slaLevel\":\"overdue\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000022\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-01T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000024\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-02T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000023\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000025\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000026\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000013\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000015\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000027\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000028\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000029\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000030\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000016\",\"serviceId\":\"SV-02\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-08T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000018\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000019\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"APPROVED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000012\",\"serviceId\":\"SV-03\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":1,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000021\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"}],\"filter\":\"all\",\"workload\":3}"
```

```
Error: off.reg1 GET /api/officer/queue?filter=all ไม่มี 1101700123456

expect(received).not.toContain(expected) // indexOf

Expected substring: not "1101700123456"
Received string:        "{\"items\":[{\"caseNo\":\"EG-2569-000020\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-11-30T16:30:00+07:00\",\"slaLevel\":\"overdue\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000022\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-01T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000024\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-02T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000023\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000025\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000026\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000013\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000015\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000027\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000028\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000029\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000030\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000016\",\"serviceId\":\"SV-02\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-08T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000018\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000019\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"APPROVED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000012\",\"serviceId\":\"SV-03\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":1,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000021\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"}],\"filter\":\"all\",\"workload\":3}"
```

```
Error: off.reg1 GET /api/officer/queue?filter=all ไม่มี 1909900555015

expect(received).not.toContain(expected) // indexOf

Expected substring: not "1909900555015"
Received string:        "{\"items\":[{\"caseNo\":\"EG-2569-000020\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-11-30T16:30:00+07:00\",\"slaLevel\":\"overdue\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000022\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-01T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000024\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-02T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000023\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000025\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000026\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000013\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000015\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000027\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000028\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000029\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000030\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000016\",\"serviceId\":\"SV-02\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-08T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000018\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000019\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"APPROVED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000012\",\"serviceId\":\"SV-03\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":1,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000021\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"}],\"filter\":\"all\",\"workload\":3}"
```

```
Error: head1 GET /api/officer/queue?filter=all ไม่มีเลข 13 หลัก

expect(received).not.toMatch(expected)

Expected pattern: not /\d{13}/
Received string:      "{\"items\":[{\"caseNo\":\"EG-2569-000020\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-11-30T16:30:00+07:00\",\"slaLevel\":\"overdue\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000022\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-01T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000024\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-02T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000010\",\"serviceId\":\"SV-03\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":2,\"owner\":null,\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000023\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000025\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000026\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000013\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000015\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000027\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000028\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000029\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000030\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000016\",\"serviceId\":\"SV-02\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-08T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000018\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000019\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"APPROVED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000012\",\"serviceId\":\"SV-03\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":1,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000021\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"}],\"filter\":\"all\"}"
```

```
Error: head1 GET /api/officer/queue?filter=all ไม่มี key idNo

expect(received).not.toContain(expected) // indexOf

Expected value: not "idNo"
Received array:     ["items", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "caseNo", "serviceId", "applicantName", "idMasked", "status", "step", "owner", "dueAt", "slaLevel", "idNo", "filter"]
```

```
Error: head1 GET /api/officer/queue?filter=all ไม่มี 3100600987659

expect(received).not.toContain(expected) // indexOf

Expected substring: not "3100600987659"
Received string:        "{\"items\":[{\"caseNo\":\"EG-2569-000020\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-11-30T16:30:00+07:00\",\"slaLevel\":\"overdue\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000022\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-01T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000024\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-02T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000010\",\"serviceId\":\"SV-03\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":2,\"owner\":null,\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000023\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000025\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000026\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000013\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000015\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000027\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000028\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000029\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000030\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000016\",\"serviceId\":\"SV-02\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-08T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000018\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000019\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"APPROVED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000012\",\"serviceId\":\"SV-03\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":1,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000021\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"}],\"filter\":\"all\"}"
```

```
Error: head1 GET /api/officer/queue?filter=all ไม่มี 1101700123456

expect(received).not.toContain(expected) // indexOf

Expected substring: not "1101700123456"
Received string:        "{\"items\":[{\"caseNo\":\"EG-2569-000020\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-11-30T16:30:00+07:00\",\"slaLevel\":\"overdue\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000022\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-01T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000024\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-02T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000010\",\"serviceId\":\"SV-03\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":2,\"owner\":null,\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000023\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000025\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000026\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000013\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000015\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000027\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000028\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000029\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000030\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000016\",\"serviceId\":\"SV-02\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-08T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000018\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000019\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"APPROVED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000012\",\"serviceId\":\"SV-03\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":1,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000021\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"}],\"filter\":\"all\"}"
```

```
Error: head1 GET /api/officer/queue?filter=all ไม่มี 1909900555015

expect(received).not.toContain(expected) // indexOf

Expected substring: not "1909900555015"
Received string:        "{\"items\":[{\"caseNo\":\"EG-2569-000020\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-11-30T16:30:00+07:00\",\"slaLevel\":\"overdue\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000022\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-01T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000024\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-02T16:30:00+07:00\",\"slaLevel\":\"near\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000010\",\"serviceId\":\"SV-03\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":2,\"owner\":null,\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000023\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg1\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000025\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000026\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-03T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000013\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000015\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000027\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000028\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000029\",\"serviceId\":\"SV-01\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000030\",\"serviceId\":\"SV-01\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"SUBMITTED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-04T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000016\",\"serviceId\":\"SV-02\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-08T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000018\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมชาย ใจดี\",\"idMasked\":\"X-XXXX-XXXXX-45-6\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1101700123456\"},{\"caseNo\":\"EG-2569-000019\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"APPROVED\",\"step\":null,\"owner\":null,\"dueAt\":\"2026-12-09T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"},{\"caseNo\":\"EG-2569-000012\",\"serviceId\":\"SV-03\",\"applicantName\":\"ปิติ มีสุข\",\"idMasked\":\"X-XXXX-XXXXX-01-5\",\"status\":\"IN_REVIEW\",\"step\":1,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"1909900555015\"},{\"caseNo\":\"EG-2569-000021\",\"serviceId\":\"SV-02\",\"applicantName\":\"สมหญิง รักไทย\",\"idMasked\":\"X-XXXX-XXXXX-65-9\",\"status\":\"IN_REVIEW\",\"step\":null,\"owner\":\"off.reg2\",\"dueAt\":\"2026-12-11T16:30:00+07:00\",\"slaLevel\":\"normal\",\"idNo\":\"3100600987659\"}],\"filter\":\"all\"}"
```

# Test source

```ts
  743 |     await reset();
  744 |     const { page: v } = await newSession(browser);
  745 |     await verifyAt(v, 'K7M2Q9XA', '2027-02-02T23:59:00+07:00', 'VALID', '2027-02-02');
  746 |     await verifyAt(v, 'K7M2Q9XA', '2027-02-03T00:00:00+07:00', 'EXPIRED', '2027-02-02');
  747 |   });
  748 | 
  749 |   await test.step('ส่วน E ออกวันที่ 29 ก.พ. 2571', async () => {
  750 |     await reset();
  751 |     await setClock('2028-02-29T10:00:00+07:00');
  752 |     const reg2 = await loginStaff('off.reg2');
  753 |     await apiApprove(reg2, caseNo(25));
  754 |     const { verifyCode: e1 } = await apiIssue(reg2, caseNo(25), 'DOC-2571-000001');
  755 |     const reg1 = await loginStaff('off.reg1');
  756 |     const { verifyCode: e2 } = await apiIssue(reg1, caseNo(19), 'DOC-2571-000002');
  757 |     const { page: v } = await newSession(browser);
  758 |     await verifyAt(v, e1, '2028-05-28T23:59:00+07:00', 'VALID', '2028-05-28');
  759 |     await verifyAt(v, e1, '2028-05-29T00:00:00+07:00', 'EXPIRED', '2028-05-28');
  760 |     await verifyAt(v, e2, '2029-02-27T23:59:00+07:00', 'VALID', '2029-02-27');
  761 |     await verifyAt(v, e2, '2029-02-28T00:00:00+07:00', 'EXPIRED', '2029-02-27');
  762 |   });
  763 | 
  764 |   await test.step('ส่วน D ลายเซ็นไม่ตรง (ตรวจก่อนวันหมดอายุ A-43)', async () => {
  765 |     await reset();
  766 |     await tamper('DOC-2569-000001');
  767 |     const { page: v } = await newSession(browser);
  768 |     await expectVerify(v, 'K7M2Q9XA', 'TAMPERED');
  769 |     await expect(tid(v, 'verify-doc-no')).toHaveCount(0);
  770 |     await expect(tid(v, 'verify-applicant')).toHaveCount(0);
  771 |     const api = await expectApi((await newApi()).get('/api/verify/K7M2Q9XA'), 200);
  772 |     expect(api.result).toBe('TAMPERED');
  773 |     expect(api.applicantMasked).toBeUndefined();
  774 |     expect(api.docNo).toBeUndefined();
  775 |     await verifyAt(v, 'K7M2Q9XA', '2027-03-01T00:00:00+07:00', 'TAMPERED');
  776 |     await expect(tid(v, 'verify-doc-no')).toHaveCount(0);
  777 |   });
  778 | });
  779 | 
  780 | // ═══════════════════════════════════ PDPA ═══════════════════════════════════
  781 | 
  782 | test('TC-PDPA-01 ปิดบังเลขบัตรบนจอ', async ({ browser }) => {
  783 |   await reset();
  784 |   const NO = caseNo(25);
  785 | 
  786 |   await test.step('off.reg2 /officer/queue', async () => {
  787 |     const { page: p } = await staffSession(browser, 'off.reg2');
  788 |     await p.goto('/officer/queue');
  789 |     await expect(tid(p, 'queue-row')).toHaveCount(17);
  790 |     const masked = (await tid(p, 'row-id-masked').allInnerTexts()).map((t) => t.trim());
  791 |     expect(masked).toHaveLength(17);
  792 |     for (const m of masked) expect(m).toMatch(MASK_RE);
  793 |     await expect(queueRow(p, NO).getByTestId('row-id-masked')).toHaveText('X-XXXX-XXXXX-65-9');
  794 |     await expect(queueRow(p, caseNo(26)).getByTestId('row-id-masked')).toHaveText('X-XXXX-XXXXX-45-6');
  795 | 
  796 |     await openOfficer(p, NO);
  797 |     await expect(tid(p, 'applicant-id')).toHaveText('X-XXXX-XXXXX-65-9');
  798 |     const html = await p.content();
  799 |     expect(html).not.toContain('3100600987659');
  800 |     expect(html).not.toContain('3-1006-00987-65-9');
  801 |   });
  802 | 
  803 |   await test.step('head1 เห็นปิดบังเหมือนกัน', async () => {
  804 |     const { page: h } = await staffSession(browser, 'head1');
  805 |     await openOfficer(h, NO);
  806 |     await expect(tid(h, 'applicant-id')).toHaveText('X-XXXX-XXXXX-65-9');
  807 |     expect(await h.content()).not.toContain('3100600987659');
  808 |   });
  809 | 
  810 |   await test.step('ประชาชนเห็นเลขเต็มของตัวเอง', async () => {
  811 |     const sy = await citizenSession(browser, ID.SOMYING);
  812 |     await openCitizen(sy.page, NO);
  813 |     await expect(tid(sy.page, 'case-id-full')).toHaveText('3-1006-00987-65-9');
  814 |     const sc = await citizenSession(browser, ID.SOMCHAI);
  815 |     await openCitizen(sc.page, caseNo(20));
  816 |     await expect(tid(sc.page, 'case-id-full')).toHaveText('1-1017-00123-45-6');
  817 |   });
  818 | });
  819 | 
  820 | test('TC-PDPA-02 API (JSON) ไม่ส่งเลขบัตรเต็ม', async () => {
  821 |   await reset();
  822 |   const URLS = [
  823 |     '/api/officer/queue?filter=all',
  824 |     `/api/cases/${caseNo(25)}`,
  825 |     `/api/cases/${caseNo(26)}`,
  826 |     `/api/cases/${caseNo(20)}`,
  827 |     '/api/notifications',
  828 |     `/api/cases/${caseNo(25)}/files`,
  829 |   ];
  830 |   for (const user of ['off.reg1', 'head1'] as const) {
  831 |     await test.step(user, async () => {
  832 |       const api = await loginStaff(user);
  833 |       for (const url of URLS) {
  834 |         const label = `${user} GET ${url}`;
  835 |         const res = await api.get(url);
  836 |         expect.soft(res.status(), label).toBe(200);
  837 |         expect.soft(res.headers()['content-type'] ?? '', label).toContain('application/json');
  838 |         const body = await bodyOf(res);
  839 |         const s = JSON.stringify(body);
  840 |         expect.soft(s, `${label} ไม่มีเลข 13 หลัก`).not.toMatch(/\d{13}/);
  841 |         expect.soft(s, `${label} ไม่มีรูปแบบ d-dddd-ddddd-dd-d`).not.toMatch(/\d-\d{4}-\d{5}-\d{2}-\d/);
  842 |         expect.soft(deepKeys(body), `${label} ไม่มี key idNo`).not.toContain('idNo');
> 843 |         for (const id of [ID.SOMYING, ID.SOMCHAI, ID.PITI]) expect.soft(s, `${label} ไม่มี ${id}`).not.toContain(id);
      |                                                                                                        ^ Error: head1 GET /api/officer/queue?filter=all ไม่มี 1909900555015
  844 |         if (Array.isArray(body.items)) {
  845 |           for (const it of body.items) if ('idMasked' in it) expect.soft(it.idMasked, `${label} items[].idMasked`).toMatch(MASK_RE);
  846 |         }
  847 |         if (url.startsWith('/api/officer/queue')) {
  848 |           expect.soft(body.items?.length, `${label} จำนวนแถว`).toBeGreaterThan(0);
  849 |           for (const it of body.items ?? []) expect.soft(it.idMasked, `${label} ${it.caseNo}`).toMatch(MASK_RE);
  850 |         }
  851 |         if (/^\/api\/cases\/EG-\d{4}-\d{6}$/.test(url)) expect.soft(body.idMasked, `${label} idMasked`).toMatch(MASK_RE);
  852 |       }
  853 |     });
  854 |   }
  855 | });
  856 | 
  857 | test('TC-PDPA-03 แสดงเลขเต็มต้องมีเหตุผลและ Audit', async ({ browser }) => {
  858 |   await reset();
  859 |   const NO = caseNo(25);
  860 |   const reg2 = await staffSession(browser, 'off.reg2');
  861 |   const p = reg2.page;
  862 |   const unmaskUrl = `/api/officer/cases/${NO}/unmask`;
  863 |   await openOfficer(p, NO);
  864 | 
  865 |   await test.step('1–2 เหตุผลว่าง / เว้นวรรคล้วน', async () => {
  866 |     for (const [label, reason] of [
  867 |       ['ว่าง', ''],
  868 |       ['เว้นวรรคล้วน', '   '],
  869 |     ] as const) {
  870 |       await uiUnmask(p, reason);
  871 |       await expect(tid(p, 'unmask-error'), label).toHaveText(MSG.REASON_REQUIRED);
  872 |       await expect(tid(p, 'full-id'), label).toHaveCount(0);
  873 |       const e = await expectApi(reg2.api.post(unmaskUrl, { data: { reason } }), 400, 'REASON_REQUIRED');
  874 |       expect(e.message).toBe(MSG.REASON_REQUIRED);
  875 |     }
  876 |   });
  877 | 
  878 |   await test.step('3 เหตุผลถูกต้อง → เห็นเลขเต็ม', async () => {
  879 |     await uiUnmask(p, 'ตรวจสอบตัวตนซ้ำ');
  880 |     await expect(tid(p, 'full-id')).toHaveText('3-1006-00987-65-9');
  881 |   });
  882 | 
  883 |   await test.step('4 โหลดหน้าซ้ำ → ปิดบังตามเดิม', async () => {
  884 |     await p.reload();
  885 |     await expect(tid(p, 'applicant-id')).toHaveText('X-XXXX-XXXXX-65-9');
  886 |     await expect(tid(p, 'full-id')).toHaveCount(0);
  887 |   });
  888 | 
  889 |   await test.step('5 Audit UNMASK 1 แถว (จับ B11)', async () => {
  890 |     const { page: a } = await staffSession(browser, 'audit1');
  891 |     const [row] = await uiAuditExpect(a, { event: 'UNMASK' }, 1);
  892 |     expect(row.actor).toBe('off.reg2');
  893 |     expect(row.role).toBe('officer');
  894 |     expect(row.caseText).toBe(NO);
  895 |     expect(row.eventText).toBe('UNMASK');
  896 |     expect(row.detail).toContain('ตรวจสอบตัวตนซ้ำ');
  897 |     expect(row.iso).toBe(T0);
  898 |   });
  899 | 
  900 |   await test.step('6 บทบาทอื่น/ประชาชนเรียก unmask → 403', async () => {
  901 |     for (const api of [await loginStaff('exec1'), await loginStaff('audit1'), await loginCitizen(ID.SOMYING)]) {
  902 |       await expectApi(api.post(unmaskUrl, { data: { reason: 'x' } }), 403);
  903 |     }
  904 |   });
  905 | });
  906 | 
  907 | // ═══════════════════════════════════ DASH ═══════════════════════════════════
  908 | 
  909 | test('TC-DASH-01 Dashboard ตัวเลขเริ่มต้น', async ({ browser }) => {
  910 |   await reset();
  911 |   const ex = await staffSession(browser, 'exec1');
  912 |   const p = ex.page;
  913 |   await p.goto('/dashboard');
  914 |   await expect(tid(p, 'period-select')).toHaveValue('2026-12');
  915 |   await expect(tid(p, 'service-select')).toHaveValue('ALL');
  916 | 
  917 |   await test.step('ALL ธ.ค. บนจอและ API', async () => {
  918 |     const k: Kpis = { received: 3, closed: 0, pct: '–', backlog: 21, overdue: 1 };
  919 |     await expectKpis(p, k);
  920 |     const d = await getDashboard(ex.api, '2026-12', 'ALL');
  921 |     expectDash(d, k);
  922 |     expect(d.ontimePct).toBeNull();
  923 | 
  924 |     const WL: Record<string, number> = { 'off.reg1': 3, 'off.reg2': 9, 'off.works1': 0 };
  925 |     await expect(tid(p, 'workload-row')).toHaveCount(3);
  926 |     for (const [u, n] of Object.entries(WL)) {
  927 |       await expect(rowBy(p, 'workload-row', 'data-username', u).getByTestId('workload-value')).toHaveText(String(n));
  928 |     }
  929 |     const wl = Object.fromEntries((d.workload as Array<{ username: string; count: number }>).map((w) => [w.username, w.count]));
  930 |     expect(wl).toEqual(WL);
  931 |   });
  932 | 
  933 |   await test.step('ไม่มีข้อมูลส่วนบุคคลบนจอ (BR-24)', async () => {
  934 |     const text = await p.locator('body').innerText();
  935 |     expect(text).not.toMatch(/\d{13}/);
  936 |     expect(text).not.toMatch(/0\d{9}/);
  937 |     expect(piiHits([text])).toEqual([]);
  938 |   });
  939 | 
  940 |   await test.step('ตัวกรองบริการ', async () => {
  941 |     const ROWS: Array<[string, Kpis]> = [
  942 |       ['SV-01', { received: 3, closed: 0, pct: '–', backlog: 11, overdue: 1 }],
  943 |       ['SV-02', { received: 0, closed: 0, pct: '–', backlog: 7, overdue: 0 }],
```