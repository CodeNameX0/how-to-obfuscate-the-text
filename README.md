# 텍스트 난독화 가이드

이 문서는 텍스트를 난독화하는 다양한 방법들을 단계별로 설명합니다.

## 1. Base64 인코딩 방법

Base64는 바이너리 데이터를 ASCII 문자로 변환하는 인코딩 방법입니다.

### 기본 원리
- 3바이트(24비트)를 4개의 6비트 그룹으로 나눕니다
- 각 6비트 값(0-63)을 Base64 문자로 매핑합니다
- 패딩이 필요한 경우 '=' 문자를 사용합니다

### 상세한 인코딩 과정 예시

**1단계: 문자를 바이너리로 변환**
```
"Cat" → ASCII 코드:
C = 67 (01000011)
a = 97 (01100001)  
t = 116 (01110100)
```

**2단계: 24비트를 6비트씩 4그룹으로 나누기**
```
010000 110110 000101 110100
  16     54     5      52
```

**3단계: 각 6비트 값을 Base64 문자로 변환**
```
16 → Q
54 → 2  
5  → F
52 → 0

결과: "Cat" → "Q2F0"
```

**더 복잡한 예시:**
```
"Hello" → "SGVsbG8="
H(72) e(101) l(108) l(108) o(111)
01001000 01100101 01101100 01101100 01101111
010010 000110 010101 101100 011011 000110 1111**
18     6      21     44     27     6      60(패딩)
S      G      V      s      b      G      8=
```

## 2. Base64 문자표

Base64에서 사용하는 64개 문자:

| 값 | 문자 | 값 | 문자 | 값 | 문자 | 값 | 문자 |
|----|------|----|----- |----|------|----|----- |
| 0  | A    | 16 | Q    | 32 | g    | 48 | w    |
| 1  | B    | 17 | R    | 33 | h    | 49 | x    |
| 2  | C    | 18 | S    | 34 | i    | 50 | y    |
| 3  | D    | 19 | T    | 35 | j    | 51 | z    |
| 4  | E    | 20 | U    | 36 | k    | 52 | 0    |
| 5  | F    | 21 | V    | 37 | l    | 53 | 1    |
| 6  | G    | 22 | W    | 38 | m    | 54 | 2    |
| 7  | H    | 23 | X    | 39 | n    | 55 | 3    |
| 8  | I    | 24 | Y    | 40 | o    | 56 | 4    |
| 9  | J    | 25 | Z    | 41 | p    | 57 | 5    |
| 10 | K    | 26 | a    | 42 | q    | 58 | 6    |
| 11 | L    | 27 | b    | 43 | r    | 59 | 7    |
| 12 | M    | 28 | c    | 44 | s    | 60 | 8    |
| 13 | N    | 29 | d    | 45 | t    | 61 | 9    |
| 14 | O    | 30 | e    | 46 | u    | 62 | +    |
| 15 | P    | 31 | f    | 47 | v    | 63 | /    |

**패딩 문자:** =

## 3-9. ASCII 코드표 (완전판)

ASCII 코드 0-127의 완전한 문자표

### 제어 문자 (0-31)
| Dec | Hex | Char | Dec | Hex | Char | Dec | Hex | Char | Dec | Hex | Char |
|-----|-----|------|-----|-----|------|-----|-----|------|-----|-----|------|
| 0   | 00  | NUL  | 8   | 08  | BS   | 16  | 10  | DLE  | 24  | 18  | CAN  |
| 1   | 01  | SOH  | 9   | 09  | TAB  | 17  | 11  | DC1  | 25  | 19  | EM   |
| 2   | 02  | STX  | 10  | 0A  | LF   | 18  | 12  | DC2  | 26  | 1A  | SUB  |
| 3   | 03  | ETX  | 11  | 0B  | VT   | 19  | 13  | DC3  | 27  | 1B  | ESC  |
| 4   | 04  | EOT  | 12  | 0C  | FF   | 20  | 14  | DC4  | 28  | 1C  | FS   |
| 5   | 05  | ENQ  | 13  | 0D  | CR   | 21  | 15  | NAK  | 29  | 1D  | GS   |
| 6   | 06  | ACK  | 14  | 0E  | SO   | 22  | 16  | SYN  | 30  | 1E  | RS   |
| 7   | 07  | BEL  | 15  | 0F  | SI   | 23  | 17  | ETB  | 31  | 1F  | US   |

### 인쇄 가능한 문자 (32-126)
| Dec | Hex | Char | Dec | Hex | Char | Dec | Hex | Char | Dec | Hex | Char |
|-----|-----|------|-----|-----|------|-----|-----|------|-----|-----|------|
| 32  | 20  | SPACE| 48  | 30  | 0    | 64  | 40  | @    | 80  | 50  | P    |
| 33  | 21  | !    | 49  | 31  | 1    | 65  | 41  | A    | 81  | 51  | Q    |
| 34  | 22  | "    | 50  | 32  | 2    | 66  | 42  | B    | 82  | 52  | R    |
| 35  | 23  | #    | 51  | 33  | 3    | 67  | 43  | C    | 83  | 53  | S    |
| 36  | 24  | $    | 52  | 34  | 4    | 68  | 44  | D    | 84  | 54  | T    |
| 37  | 25  | %    | 53  | 35  | 5    | 69  | 45  | E    | 85  | 55  | U    |
| 38  | 26  | &    | 54  | 36  | 6    | 70  | 46  | F    | 86  | 56  | V    |
| 39  | 27  | '    | 55  | 37  | 7    | 71  | 47  | G    | 87  | 57  | W    |
| 40  | 28  | (    | 56  | 38  | 8    | 72  | 48  | H    | 88  | 58  | X    |
| 41  | 29  | )    | 57  | 39  | 9    | 73  | 49  | I    | 89  | 59  | Y    |
| 42  | 2A  | *    | 58  | 3A  | :    | 74  | 4A  | J    | 90  | 5A  | Z    |
| 43  | 2B  | +    | 59  | 3B  | ;    | 75  | 4B  | K    | 91  | 5B  | [    |
| 44  | 2C  | ,    | 60  | 3C  | <    | 76  | 4C  | L    | 92  | 5C  | \    |
| 45  | 2D  | -    | 61  | 3D  | =    | 77  | 4D  | M    | 93  | 5D  | ]    |
| 46  | 2E  | .    | 62  | 3E  | >    | 78  | 4E  | N    | 94  | 5E  | ^    |
| 47  | 2F  | /    | 63  | 3F  | ?    | 79  | 4F  | O    | 95  | 5F  | _    |

| Dec | Hex | Char | Dec | Hex | Char |
|-----|-----|------|-----|-----|------|
| 96  | 60  | `    | 112 | 70  | p    |
| 97  | 61  | a    | 113 | 71  | q    |
| 98  | 62  | b    | 114 | 72  | r    |
| 99  | 63  | c    | 115 | 73  | s    |
| 100 | 64  | d    | 116 | 74  | t    |
| 101 | 65  | e    | 117 | 75  | u    |
| 102 | 66  | f    | 118 | 76  | v    |
| 103 | 67  | g    | 119 | 77  | w    |
| 104 | 68  | h    | 120 | 78  | x    |
| 105 | 69  | i    | 121 | 79  | y    |
| 106 | 6A  | j    | 122 | 7A  | z    |
| 107 | 6B  | k    | 123 | 7B  | {    |
| 108 | 6C  | l    | 124 | 7C  | \|   |
| 109 | 6D  | m    | 125 | 7D  | }    |
| 110 | 6E  | n    | 126 | 7E  | ~    |
| 111 | 6F  | o    | 127 | 7F  | DEL  |

## 10. 문자 치환 방법

Base64 결과에서 특정 문자를 다른 문자로 바꿉니다.

### 치환 규칙
- a → #
- e → @  
- i → !
- o → $
- u → ^

### 예시
```
"aGVsbG8=" → "#GVsb G8="
```

### 사용 방법
1. 먼저 텍스트를 Base64로 인코딩
2. 결과에서 모음을 특수문자로 치환
3. 더 복잡한 난독화 효과

## 11. 역변환과 보안 고려사항

### 주의사항
1. 단순 치환은 빈도 분석으로 해독 가능
2. Base64는 인코딩이지 암호화가 아님
3. 패턴 분석으로 쉽게 해독될 수 있음

### 보안 강화 방법
- 여러 방법을 조합하여 사용
- 키를 사용한 암호화 추가
- 무작위 패딩 삽입
- 다층 인코딩 적용

## 12. 요약 및 활용 방법

### 텍스트 난독화 방법들

#### 1. Base64 인코딩
- **용도:** 간단한 텍스트 숨김, 데이터 전송
- **장점:** 표준화됨, 쉬운 구현
- **단점:** 쉽게 디코딩됨

#### 2. ASCII 코드 변환
- **용도:** 숫자 형태로 텍스트 표현
- **장점:** 직관적이지 않음
- **단점:** 패턴이 명확함

#### 3. 문자 치환
- **용도:** 간단한 암호화
- **장점:** 다양한 방법 가능
- **단점:** 빈도 분석에 취약

### 실제 활용
- 소스코드 난독화
- 간단한 데이터 숨김
- 교육용 암호화 예제
- 퍼즐이나 게임

### 보안이 중요한 경우
- AES, RSA 등 강력한 암호화 사용
- 해시 함수 활용
- 디지털 서명 적용

---

**작성일:** 2025년 8월 1일  
**목적:** 교육용

---

## 번외편
- 이 글을 난독화하면? ㅋㅋㅋㅋ
```
pqJ7hyJ7QWr6g$!K6EI$snqqrr!KgACI82J7xAClbyOOgQYhrXjMwIDIq$!O82J7xSI7R6J7q$CIg0SLtACIpqJ7BCK7gU$qrzJhsDC^E2OgnyOlU^OItASq#yOnZ2OIY!I7$WZ7gw5!sTbltDSLgkqmszqgsDClZ2O^Y2OlVyOIcWZ7lC66VCr6gE7krDSQTJFIsMVRBBSLgArms3rsqDCnV2Ol#y@kkyOI02J7IWJ70O76gMyIjACIE6J7MKr6ggpgrTbnsDppszbjtDSLgwJ$sjImsDClZ2O^Y2OlVyOIpqJ7hyJ7QWr6g0CIAmr6$!I7gALhtTbnsDbjrDCnV2OqL^OhwqOItAClZ2@hP^OnC^OIcO56U2L7kqI7M#I7g0CIpqJ7cmZ7gwJ$sT6!sDyIjMCIg0blsj6tsDCkXy@nEyOh2^OIE+46Im76g$!K6AJ$sj6!rr!Kg0CIlq46ACr6gUpsrnKsrDCnV2@kWyOpL^OIq$!OQCK7l6J7q$CItAClZ2O^Y2OlVyOIcWZ7$^46ECr6g$!K6Q4jrnqmsr!Kg0CIYmZ7YmL7gApnsjLrrD!LzAyIjMyIgACqV2@lZ2@hq^OI02J70SY7$yY7g$!K6AJ$sj6!rr!Kg0CIM2J7KWJ7gA4psTbnsHI$sDItqH4psD!Kq$Dkgy@p@y^KqASLgQImtzZktDC^K2OpKy@jF2OIcG66cOY7V!Z7gApnsvK!sD!Kq$DhP^@q#y^KqASLggZmtD4srDCnT^Ol9yOIJl0QTFEI^IDIjMyIjACI$C56pS56U2L7US56gw$sq3b!sD!Kq$DkgyOqL^^KqASLgQImtz#tqDCt#yOrJyOIsgKkrTZmtDIpszZktD!Kq$Dkgy@p@y^KqASLgEqhsTI$sDCsE2OtdyOsN^OIsAY^qjK!sDC^K2OpKy@jF2OIcWZ7$^46ECr6g$!K6Q4jrnqmsr!Kg0CIpS56U2L742J7gQjNlNXYCB!LxAyIjMyIgACpT^@ly^@qw^OIUmZ7F+46cK46ggr!tTq!s3YhtDyIjMCIgUpsrnKsrDSq#yOnZ2OIPC76g0blsTpmsD!LyEDIjMCIgkqmsHI$sDSqU^Ol9yO^dyOI1!L7k^46g0CIF6J79KI7gkKlrjKjtDChcy@k@yOts^OItACgwqOl2yOIUmZ74!Z7UWJ7gwZltnqmszqgsDCvl^OpC2OItASq#yOrCyOIs@J7YWZ7pWZ7wGK7gQYnsXpsrnKsrDCrf^OrXyOItASly^@qw^OIUmZ7VCr6ggYlsT7srDyIjMCIgwYnsj$nsDCmIyOIgC56F+460WZ7gw$sq3b!sDCnh^Ovcy@nEyOh2^OI0SY7$yY7g4yMgg5!rTYlsDCgwqOlZ2O^Y2OlVyOIA@K702J7pS56U2L742J7gQp!rTjNlNXYCB!LyASpK^OgwqOIF+460WZ7gwZ$rzLns3JhsT$trDChP^O!5^OIA2J7YmZ7YmL7gwJ!sj6!rD!LxASrV2OrCyOmdyOvjyOIjMyIgASrV2OrCyOpg^O$zqOIIWJ70O76gw7sqjZmtD4sr36lsD!LxEDIjMCIgw7sqjqmtDClZ2@hP^OnC^OIcWZ7h6J71O76gQZjrD!LzACmZ2Om5yOIcG66Q6J74y66Y!I75qY7gQYnszYnsjqqrDCnEyOkXyOvzqOsyqOI^IDIpS56U2L742J7gwZ$rTjNlNXYCBCvl^O^K2OpKy@jF2OIACK78!66g4SMgUpsrnKsrDSq#yOrCyOIjMyIgACYgBGI!0DOHB!YzZ1RjICIS#$4gISP4ckYzZ1RhJCIgBGYgw5!sjImsDyIjMCIg4FIS#$4gUHItACJgIph!Dybg0CIhA!kGKOIpBSLgACIAB!kGKOIlBSLgMCIS#$4gEGItASm5yOn3qOIYmZ7YmL7gMyIjACI^Q6!rj4!rn4vqTJsrDCnh^Ok@yO^s^OI4W66k^46gwbprDpnsjLrrDSlgy@^K2OIcSI7Q@J78Or6wKr6gQjNlNXYCBCIVK76pC76ggZmtjZ^sDCk@yO^s^OI^ATMgMyIgACfgACTFREI8BCIGdDI8ByNyEDI8BCIgAybgwHIgYkNgwHIxETMgwHI8BCIgA!fgwHIgU0NgwHI2ITMgwHIgACI^BCfgASR2ACfgATMxACfgwHIgACI9BCfgACR3ACfgUjMxACfgACIg0GI8BCIEZDI8BSOwEDI8BCfgACI8xFI8BCIDdDI8BCNyEDI8BCIgACbgwHIgMkNgwHI4ATMgwHI8BCIgAy@gwHIgI0NgwHIzITMgwHIgACIrBCfgA!Q2ACfgcDMxACfgwHIgACI6BCfgASQ3ACfgIjMxACfgACIg$GI8BCIBZDI8B!NwEDI8BCfgACIgkHI8BCI5cDI8BSMyEDI8BCIgAS#gwHIgkjNgwHI1ATMgwHI8BCIgAC@gwHIggzNgwHIwITMgwHIgACI$BCfgACO2ACfgQDMxACfgwHIgACI3BCfgAyN3ACfgkTMxACfgACIgcGI8BCI3YDI8ByMwEDI8BCfgACIgYHI8BCI2cDI8BCOxEDI8BCIgA!ZgwHIgYjNgwHIyATMgwHI8BCIgASdgwHIgUzNgwHI3ETMgwHIgACIlBCfgASN2ACfgEDMxACfgwHIgACI0BCfgACN3ACfgYTMxACfgACIgQGI8BCI0YDI8BCMwEDI8BCfgACIgMHI8BCIzcDI8BSNxEDI8BCIgAyYgwHIgMjNgwHIgkTOgwHI8BCIgA!cgwHIgIzNgwHI0ETMgwHIgACI!BCfgA!M2ACfgACO5ACfgwHIgACIxBCfgASM3ACfgMTMxACfgACIgEGI8BCIxYDI8BCI3kDI8BCfgACIgAHI8BCIwcDI8B!MxEDI8BCIgACYgwHIgAjNgwHIgYTOgwHI81SLt0SLtwXLt0SLtwXLt0SLtwXLt0SLt0Cft0SLt0Cft0SLt0CfgwHIyFG#DBCfggXZIBCfgMWZEBCfgIXY$NEI8BC@lhEI8ByYlREI8BCI8BCIgAyXgwHIgYUNgwHIgUTOgwHIgACIPBCfgA!R0ACfgASO3ACfgACIg8DI8BCIGNDI8BCIzYDI8BCIgAyLgwHIgYkMgwHIgcDNgwHI8BCIgA!XgwHIgUUNgwHIgQTOgwHIgACIOBCfgASR0ACfgACO3ACfgACIg4DI8BCIFNDI8BCIyYDI8BCIgA!LgwHIgUkMgwHIgYDNgwHI8BCIgASXgwHIgQUNgwHIgMTOgwHIgACINBCfgACR0ACfgAyN3ACfgACIg0DI8BCIENDI8BCIxYDI8BCIgASLgwHIgQkMgwHIgUDNgwHI8BCIgACXgwHIgMUNgwHIgITOgwHIgACIMBCfgAyQ0ACfgA!N3ACfgACIgwDI8BCIDNDI8BCIwYDI8BCIgACLgwHIgMkMgwHIgQDNgwHI8BCIgAyWgwHIgIUNgwHIgETOgwHIgACILBCfgA!Q0ACfgASN3ACfgACIgsDI8BCICNDI8BCI5UDI8BCIgAyKgwHIgIkMgwHIgMDNgwHI8BCIgA!WgwHIgEUNgwHIgATOgwHIgACIKBCfgASQ0ACfgACN3ACfgACIg$DI8BCIBNDI8BCI4UDI8BCIgA!KgwHIgEkMgwHIgIDNgwHI8BCIgASWgwHIgkTNgwHIgkDOgwHIgACIJBCfgASO0ACfgAyM3ACfgACIgkDI8BCI5MDI8BCI3UDI8BCIgASKgwHIgkjMgwHIgEDNgwHI8BCIgACWgwHIggTNgwHIggDOgwHIgACIIBCfgACO0ACfgA!M3ACfgACIggDI8BCI4MDI8BCI2UDI8BCIgACKgwHIggjMgwHIgADNgwHI8BCIgAyVgwHIgcTNgwHIgcDOgwHIgACIHBCfgAyN0ACfgASM3ACfgACIgcDI8BCI3MDI8BCI1UDI8BCIgAyJgwHIgcjMgwHIgkzMgwHI8BCIgA!VgwHIgYTNgwHIgYDOgwHIgACIGBCfgA!N0ACfgACM3ACfgACIgYDI8BCI2MDI8BCI0UDI8BCIgA!JgwHIgYjMgwHIggzMgwHI8BCIgASVgwHIgUTNgwHIgUDOgwHIgACIFBCfgASN0ACfgASO2ACfgACIgUDI8BCI1MDI8BCIzUDI8BCIgASJgwHIgUjMgwHIgczMgwHI8BCIgACVgwHIgQTNgwHIgQDOgwHIgACIEBCfgACN0ACfgACO2ACfgACIgQDI8BCI0MDI8BCIyUDI8BCIgACJgwHIgQjMgwHIgYzMgwHI8BCIgAyUgwHIgMTNgwHIgMDOgwHIgACIDBCfgAyM0ACfgAyN2ACfgACIgMDI8BCIzMDI8BCIxUDI8BCIgAyIgwHIgMjMgwHIgUzMgwHI8BCIgA!UgwHIgITNgwHIgIDOgwHIgACICBCfgA!M0ACfgA!N2ACfgACIgIDI8BCIyMDI8BCIwUDI8BCIgA!IgwHIgIjMgwHIgQzMgwHI8BCIgASUgwHIgETNgwHIgEDOgwHIgACIBBCfgASM0ACfgASN2ACfgACIgEDI8BCIxMDI8BCI5QDI8BCIgASIgwHIgEjMgwHIgMzMgwHI8BCIgACUgwHIgATNgwHIgADOgwHIgACIABCfgACM0ACfgACN2ACfgACIgADI8BCIwMDI8BCI4QDI8V0QBB1UgwHIgAjMgwHIgIzMgwHI81SLt0SLtwXLt0SLtwXLt0SLtwXLt0SLt0Cft0SLt0Cft0SLt0Cft0SLt0SL81SLt0SL81SLt0SL81SLt0SLtwXLt0SLtwXLt0SLtwHI8B!chh2QgwHI4VGSgwHIjVGRgwHIyFG#DBCfggXZIBCfgMWZEBCfgIXY$NEI8BC@lhEI8ByYlREI8B!chh2QgwHI4VGSgwHIjVGRgwHIpYjMx0!MzgCIQ6J74y66gwZltXq!rDIsqDChHyO^dyOIjMyIgACfgACITVFI8BCIGFDI8BCIxMDI8BCICRVRgwHIgcTMgwHIgMjMgwHIgASSTBCfgA!RwACfgASNxACfgACTFJEI8BCI3ADI8BCIgcDI8BCfgACITJFI8BCIFFDI8BCIwMDI8BCIOl1UgwHIgYTMgwHIgIjMgwHIgAyTTBCfgASRwACfgACNxACfgAySDFEI8BCI2ADI8BCIgYDI8BCfgACITdEI8BCIEFDI8BCI5IDI8BCILFkTgwHIgUTMgwHIgEjMgwHIgA!UDBCfgACRwACfgAyMxACfgASUOVEI8BCI1ADI8BCIgUDI8BCfgACITZEI8BCIDFDI8BCI4IDI8BCI0MERgwHIgQTMgwHIgAjMgwHIgA!RGBCfgAyQwACfgA!MxACfgACVPVEI8BCI0ADI8BCIgQDI8BCfgAyQTVEI8BCICFDI8BCI3IDI8BCIzMERgwHIgMTMgwHIgkTMgwHIgACVWBCfgA!QwACfgASMxACfgACWUVEI8BCIzADI8BCIgMDI8BCfgA!QVNFI8BCIBFDI8BCI2IDI8BCIyMERgwHIgITMgwHIggTMgwHIgA!RMBCfgASQwACfgACMxACfgACWUNFI8BCIyADI8BCIgIDI8BCfgACINVEI8BCI5EDI8BCI1IDI8BCIxMERgwHIgETMgwHIgcTMgwHIgIUQUBCfgASOwACfgACI5ACfgACSPNFI8BCIxADI8BCIgEDI8BCfgA!TBNEI8BCI4EDI8BCI0IDI8BCIFxERgwHIgATMgwHIgYTMgwHIgAyUCBCfgACOwACfgACI4ACfgACTV5EI8BCIwADI8BCIgADI8BCft0SLt0SL81SLt0SL81SLt0SL81SLt0SLtwXLt0SLtwXLt0SLtwXLt0SLt0Cft0SLt0Cft0SLt0Cft0SLt0SL81SLt0SL81SLt0SL8BCfgIXY$NEI8BC@lhEI8ByYlREI8B!chh2QgwHI4VGSgwHIjVGRgwHIyFG#DBCfggXZIBCfgMWZEBCfgIXY$NEI8BC@lhEI8ByYlREI8BSKxMTLwgCIQ6J74y66gQrlszJ$sDyIjMCIgwZktDpnsjLrrDCnV2OhgyOhZyOIY2J73ITMtADIcO56U2L7gkUSDNVQgASKQyY7ECK7EmJ7$ACnR2OnT^Ol9yOIJl0QTFEI^kTLzAyIjACI9A!Kq$Dk@yO^s^OIpS56$yY7q$CIgwHIgACIvACfgMjNgwHIgACI2BCfgcDNgwHIgACImBCfgEzMgwHIgACIQBCfgUTMgwHI8BCIgAyKgwHIyYDI8BCIgASdgwHI2QDI8BCIgASZgwHIwMDI8BCIgAyTgwHI0EDI8BCfgACIgkDI8BSM2ACfgACIgQHI8BSN0ACfgACIgQGI8BSOyACfgACIg4EI8ByMxACfgwHIgACI4ACfgAjNgwHIgACIzBCfgQDNgwHIgACIjBCfggjMgwHIgACINBCfgITMgwHI8BCIgAyNgwHI5UDI8BCIgA!cgwHIzQDI8BCIgA!YgwHI3IDI8BCIgACTgwHIxEDI8BCfgACIgYDI8BCO1ACfgACIgEHI8B!M0ACfgACIgEGI8B!NyACfgACIgsEI8BCMxACfgwHIgACI1ACfgcTNgwHIgACIwBCfgEDNgwHIgACI#BCfgUjMgwHIgACIKBCfgASOgwHI8BCIgACNgwHI2UDI8BCIgAybgwHIwQDI8BCIgASWgwHI0IDI8BCIgASSgwHIggDI8BCfgACIgMDI8BSN1ACfgACIg4GI8BSOzACfgACIggFI8ByMyACfgACIggEI8BCI3ACfgwHIgACIyACfgQTNgwHIgACItBCfggzMgwHIgACIXBCfgIjMgwHIgACIHBCfgA!NgwHI8BCIgASMgwHIzUDI8BCIgACbgwHI3MDI8BCIgA!VgwHIxIDI8BCIgA!RgwHIgUDI8BCfgACIgADI8B!M1ACfgACIgsGI8B!NzACfgACIgUFI8BCMyACfgACIgUEI8BCI0ACfgwHIgACI6BCfgETNgwHIgACIqBCfgUzMgwHIgACIUBCfgkTMgwHIgACIEBCfgAyMgwHI8BCIgAS@gwHIwUDI8BCIgAS#gwHI0MDI8BCIgAyUgwHI4EDI8BCIgAyQgwHIgIDI8BCfgACIggHI8BSO0ACfgACIggGI8ByMzACfgACIgIFI8ByNxACfgACIgIEI8BCIxACfgwHIgACI3BCfggDNgwHIgACInBCfgIzMgwHIgACIRBCfgYTMgwHIgACIBBCfgACMgwHI8BSLt0SLtwXLt0SL81SLt0SLtwXLt0SL8BSLt0SLtwXLt0SL81SLt0SLtwXLt0SL8BCfgApnsjLrrDCfgIJsqDCfgApnsjLrrDCfgIJsqDCfgApnsjLrrDCfgIJsqDCfgApnsjLrrDCfgIJsqDCfgA!OQ6J74y66gwJsqTjNgQp!rjZltnqmszqgsDCnEyOkXyON2U2chJEIgwZktDpnsjLrrDCN2U2chJEI^IDIjMCIgAGYgBSP4ACIgACIgcEIgACIgA!YgACIgACIzBCIgACIgYFIgACIgAyRgACIgACITBSKpS56$yY7$AjNgACIgACI2ACIgACI3IDIgACIgQDNgACIgASMyACIgACIgYDIgACIggTMg$!KxETMxACMxEDMwADIxEDMxEDMgADMxEDMxASMwEDMxADIwETMwADMgATMwATMwASMxETMwETMwACMwETMwETMwACMwETMwETMwASMwEDMwETMwACMwATMwATMwASKxETM$8GIpgDMxgCbgkCOwEDKsBSKxATM$UGIpIzN$gEI!0DOHJ2cWd0U!A!kGKOI!8GbsVGS!ACYgBGIq$!Oc^I7I!J7gwZltHqnsX7srDClN^^KqACIgBGYgICMGJTU!A!kGKOI!QXYDJCI6w7sqDrsqDCIwA!kGKOIyUDIGB!kGKOIgUDIgA!MgIph!DCN1ASUgIph!D!NxACYgBGIq$CmZ2Ogz^OIcG66Q6J74y66gQjNlNXYCBChdy^kwqOI4qY7Em762ASgwqOI6Q4sqj6!rPjKqACIgBGYgITNgACIgACI1ACIgACI0UDIgACIgYTMgACIwATMwETMgEDMxADMwACMxEDMxEDIwADMwEDMgAGYgB!KqAL^qTI!rjpgrDCnh^Ovcy@^j^O^3qONgkKlsjr!tTY^rbDI8W664qY7Em760IDI6Q4sqj6!rLjKqACIgBGYgkCMwEDMxETMwgCI2ETMg0DI0BCIgkSMwADMwETMwgCI3kDI9ASYgkSMxADMwATMwgCI3YDI9AyQg$DnT^Ol9yOIJl0QTFEIS#$4gICdhNkIgAGYgB!KqgZmtD4srDCnh^Orm^O!E^OtdyOlw^OI8W66Q6J74y66g$DhzqOqL^@Mq$CIgw5!sjImsDSlgyOvzqOIpS56U2L742J7gwZltjLhsH4gsDyIjMCIgQ6!rj4!rn#ltnqmszqgsDCvl^Ok@yO^s^OIn0zJgArms3rsqDCnV2Ol#yOhV2OI02J7pS56$yY7g0CIk^46I^46pWZ7RWZ7k@66gwZ$rDpnsjLrrDCN2U2chJEIE2J7pMjNtADKSCr6ggr!tTY^rbDIBCr6g0CIk^46I^46V!46YK46gwZ$rzLnsn7$rj7tqDC^K2Oh5^^NggZnszJsqTDI8W66pgr!tTY^rTjM$gr!tTbnsTJsrPDItACrm^OkbyOI4O76w!r6gMyIjACI^Q6!rj4!rX$nsXpsrnKsrDSqU^Ol9yO^dyOIUq46YWZ7YmZ7AO76gwZ$rDpnsjLrrDSSJN0UBBCvl^OsE2OtdyOsN^OIs#66IS4602J7UC76gQp!rTjNlNXYCBCIVK76pC76gkKlrTZvsjbnsDCN2U2chJEI^EDIjMCIg4CpL^O!L^@qV2@hq^OpEyOIcG66EO76EOr6$^46gQYnsT6krXpsrnKsrDCnV2@kWyOpL^OIUq46YWZ7UmZ7F+46cK46gwbprjr!tTq!s3YhtDClK^OnEyO^s^OI02J7gACnT^OtdyOgwqOIUmZ7F+46cK46ggr!tTq!s3YhtDyI
```
엄...
전 갑니다
---
