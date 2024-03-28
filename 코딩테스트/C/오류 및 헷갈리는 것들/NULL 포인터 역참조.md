
```c
NameCard* MakeNameCard(char* name, char* phone) {
	NameCard* temp;
	temp = (NameCard*)malloc(sizeof(NameCard));
	if (temp == NULL) return NULL;
	strcpy_s(temp->name, sizeof(*name), name);
	strcpy_s(temp->phone,sizeof(*phone),phone);
	
	return temp;
}
```

여기에서 if문을 빼면 널포인터 역참조가 뜬다 
왜 `if`문을 제거하면 NULL 포인터 역참조 오류가 발생하는지에 대한 이유는, `malloc` 함수가 메모리 할당에 실패하면 `NULL` 포인터를 반환하기 때문입니다. 따라서 `malloc` 함수의 반환값을 검사하여 `NULL`인지 확인하고, `NULL`일 경우에는 추가적인 메모리 할당 및 초기화 작업을 진행하지 않아야 합니다.