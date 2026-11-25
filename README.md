# -Drug-administration-cycle-calculation-program

# ==========================================
# 약물 투여시 투여주기 계산 프로그램
# ==========================================

# 1. 환자 정보 및 약물 계산 요소 입력

patient_name = input("환자 이름을 입력하세요: ")
age = int(input("나이를 입력하세요: "))
weight = float(input("몸무게(kg)를 입력하세요: "))
height = float(input("키(cm)를 입력하세요: "))

drug_name = input("약물 이름을 입력하세요: ")

# 학습용 가상 계산 요소
half_life = float(input("가상 약물 반감기(시간)를 입력하세요: "))
reference_interval = float(input("기준 투여주기(시간)를 입력하세요: "))

# 투약 후 경과시간 입력
elapsed_time = float(input("마지막 투약 후 흐른 시간(시간)을 입력하세요: "))


# 2. 입력받은 환자 및 약물 정보를 리스트로 정의

patient_info = [
    patient_name,
    age,
    weight,
    height,
    drug_name,
    half_life,
    reference_interval
]


# 3. 약물 투여주기 계산 함수
# 입력 요소들을 매개변수로 전달받고
# 계산 결과를 리스트로 반환

def calculate_interval(
    weight,
    height,
    age,
    half_life,
    reference_interval
):

    # BMI 계산 (환자 정보 참고용)
    bmi = weight / ((height / 100) ** 2)

    # 학습용 기준값을 이용한 가상 계산
    # 실제 약물 투여주기 계산식이 아님
    calculated_interval = reference_interval

    # 계산 결과 리스트 반환
    result = [
        round(bmi, 2),
        calculated_interval
    ]

    return result


# 4. 투약까지 남은 시간 계산 함수

def calculate_remaining_time(
    calculated_interval,
    elapsed_time
):

    remaining_time = calculated_interval - elapsed_time

    # 경과시간이 기준주기 이상이면 0으로 표시
    if remaining_time < 0:
        remaining_time = 0

    return remaining_time


# 5. 계산하기 실행

calculation_result = calculate_interval(
    weight,
    height,
    age,
    half_life,
    reference_interval
)

bmi = calculation_result[0]
drug_interval = calculation_result[1]

remaining_time = calculate_remaining_time(
    drug_interval,
    elapsed_time
)


# 6. 결과 출력

print("\n===================================")
print("       약물 투여시 투여주기 계산 프로그램")
print("===================================")

# 투약주기 및 남은 시간 출력
print(
    f"학습용 기준 투여주기: {drug_interval}시간"
)

print(
    f"계산된 남은 시간: {remaining_time}시간"
)


# 7. 65세 이상 조건 판단

if age >= 65:
    print("\n[주의사항]")
    print("나이가 65세 이상임으로 약물투여에 주의가 필요합니다.")


# 8. 반복문(for문)을 이용한 환자 차트 출력

chart_titles = [
    "환자 이름",
    "나이",
    "몸무게",
    "키",
    "약물 이름",
    "약물 반감기",
    "기준 투여주기",
    "투약 후 경과시간",
    "BMI"
]

chart_values = [
    patient_name,
    f"{age}세",
    f"{weight}kg",
    f"{height}cm",
    drug_name,
    f"{half_life}시간",
    f"{reference_interval}시간",
    f"{elapsed_time}시간",
    bmi
]

print("\n========== 환자 차트 ==========")

print("{:<20} | {:<20}".format("항목", "입력 정보"))
print("-" * 45)

for i in range(len(chart_titles)):
    print(
        "{:<20} | {:<20}".format(
            chart_titles[i],
            chart_values[i]
        )
    )

print("=" * 45)


# 9. 최종 투약 관련 메시지 출력

print("\n========== 계산 결과 ==========")

print(
    f"학습용 기준 투여주기: {drug_interval}시간"
)

print(
    f"기준 주기까지 남은 시간: {remaining_time}시간"
)

print("===================================")
