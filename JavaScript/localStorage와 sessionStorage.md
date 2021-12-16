# localStorage VS sessionStorage
웹 스토리지 객체인 `localStorage`와 `sessionStorage`는 브라우저 내에 키-값 형태의 데이터를 저장할 수 있습니다. 페이지를 새로고침(`sessionStorage`)하거나 브라우저를 다시 실행(`localStorage`)해도 데이터가 사라지지 않고 남아있습니다.

# 메서드와 프로퍼티
- `setItem(key, value)`: 키-값을 스토리지에 저장합니다.
- `getItem(key)`: 키에 매핑된 저장된 값을 가져옵니다.
- `removeItem(key)`: 키에 매핑된 저장된 값을 삭제합니다.
- `clear()`: 모든 저장 값을 삭제합니다.
- `key(index)`: `index`에 해당하는 키를 가져옵니다.
- `length`: 저장된 값의 개수를 가져옵니다.
