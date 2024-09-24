# API 명세서

| 구분 | API 명 | 설명 |
| --- | --- | --- |
| 정보 저장 | 출석 체크 | 출석 시 시간을 저장합니다. |
| 정보 조회 | 출석 기록 조회 | 연간, 월간 출석정보를 확인합니다. |

# 출석 체크 API

## Request

| 메서드 | 요청 URL |
| --- | --- |
| POST | /api/attendance/checkIn |

## Body

```json
{
"student_name": "string",
"student_id" : "string", //학생 식별 정보
"timestamp" : "string" // 예: "2024-09-24T10:00:00"
}
```

## Response

200 OK

```json
{
"message": "Check-in successful",
"check_in_time": "string"  // 실제 체크인 시간 반환
}
```

400 BAD REQUEST

```json
{
"message": "Check-in fail",
"check_in_time": "string"  // 실제 체크인 시간 반환
}
```

405 wrong position

```json
{
"message": "Check-in is not available",
"check_in_time": "string"  // 실제 체크인 시간 반환
}
```

# 출석 기록 조회 API

| 메서드 | 요청 URL |
| --- | --- |
| POST | /api/attendance/showMonth |

## Body

```json
{
	"student_id" : "string", //관리자 id 만 열람가능
	"Month" : "short" //(0~12) 0 입력 시 현재년도의 전체기록 
}
```

## Response

200 OK

```json
{
	"student_id": "string",
	"attendance_records": [{
		"date": "string",       // 예: "2024-09-24"
		"check_in_time": "string" // 예: "10:00:00"
		}]
}
```

204 Non Content

```json
{
	"student_id": "string",
	"message": "Non Content"
}
```

400 BAD REQUEST

```json
{
	"student_id": "string",
	"message": "not available"
}
```