1. reactjs là 1 thư viên hổ trọ người dùng tạo giao diện
2. trong mô hình MVC thì reactjs là view
3. cách thức hoat động chạy cũng reactjs khi chayj lên yarn start || npm start thì sẽ chạy file index.html trong thư mục public. trong file index.html có 1 thể div có id là root. Code viết trong src đều với mục đích là render vào thẻ có id root này.
4. props là 1 đối tương lưu giá trị của 1 thuộc tính
5. event là sự kiện xay ra, sẽ có 1 phương thức của component được gọi. ví dụ như onClick, onChange. nếu event được gọi kèm theo tham số thì function phải viết kiểu arrow function
6. ref dùng để lấy tham chiếu đến 1 node DOM ví dụ ở 1 thể input khai báo 1 ref có tên là abc thì ở 1 event onclick show ra giá trị nhập vào input thì chúng ta chỉ cần gọi đến this.refs.abc
7. state là trang thái. Ví dụ sau khi bấm vào button thì muốn ẩn 1 danh sách. state khác với props là props không thể set giá trị được
8. Lifecycle vòng đời

- mounting: (khởi tạo)
  - constructor() hàm tạo
  - componentWillMount() ta có thể thay đổi state trước khi render
  - render() hàm render dự liệu
  - componentDidMount() sau khi render ta có thể tương tác lên các thành phần đã render ra rồi ví dụ dùng jquery để thay đổi màu sắc, phông chữ ...
- updating

  - componentWillReceiveProps() để update state với param truyền vào method là nextProps
  - shouldComponentUpdate() Nhận kq props hoặc là state thay đổi là nextProps, nextStates
  - componentWillUpdate() sẽ cập nhật
  - render()
  - componentDidUpdate() cập nhật thành công
    ps: componentWillReceiveProps đã được thay thế bằng getDerivedStateFromProps Nó sẽ call mỗi khi component created hoặc mỗi lần khi thay đổi props hoặc state

- unMounting
  - componentWillUnMount() Phương thức này được gọi khi một thành phần đang bị xóa khỏi DOM

9. React hook thay vì viết code sử dụng class kiểu OPP thì React hook viết theo kiểu Functional Programming để giảm khối code

Basic Hook

- useState hàm này nhận đầu vào là giá trị khởi tạo của 1 state và trả ra 1 mảng gồm có 2 phần tử, phần tử đầu tiên là state hiện tại, phần tử thứ 2 là 1 function dùng để update state

ví dụ: const[ isLoading, setLoading] = useState(false);
onClick() {
setLoading(true)
}

- useEffect sẽ thay thế với các hàm componentDidMount, componentDidUpdate và componentWillUnMount trong LifeCycle
  Để tránh việc hàm useEffect luôn chạy vào mỗi khi có thay đổi State thì ta có thể truyền vào tham số thứ 2 trong useEffect đó là 1 array, trong array này ta có thể truyền vào đó những giá trị mà useEffect sẽ subcribe nó, tức là chỉ khi nào những giá trị đó thay đổi thì hàm useEffect mới được thực thi.
  Ví du: useEffect(
  () => {
  const subscription = props.source.subscribe();
  return () => {
  subscription.unsubscribe();
  };
  },
  [props.source], // giá trị được subcrive
  );

Additional Hooks

- useReducer nhận vào một reducer dạng (state, action) và trả ra một newState. Khi sử dụng chúng ta sẽ nhận được một cặp bao gồm current state và dispatch function

- useMemo nó khá giống với hàm shouldComponentUpdate trong LifeCycle. Bằng cách truyền vào 1 tham số thứ 2 thì chỉ khi tham số này thay đổi thì thằng useMemo mới được thực thi. Ví dụ trong các lọc sản phẩm

- useCallback có nhiệm vụ tương tự như useMemo nhưng khác ở chỗ function truyền vào useMemo bắt buộc phải ở trong quá trình render trong khi đối với useCallback đó lại là function callback của 1 event nào đó như là onClick chẳng hạn

Saga

- put: Có nhiệm vụ dispatch 1 action
- call: Dùng để call 1 function. Nếu nó return về một promise, tạm dừng saga cho đến khi promise được giải quyết
- takeEvery: Thực thi và trả lại kết quả của mọi actions được gọi.
- takeLatest: Nếu chúng ta thực hiện một loạt các actions, nó sẽ chỉ trả lại kết quả của actions cuối cùng.
- Select: Call 1 selector để lấy data từ store.
- fork: Thực hiện một hoạt động non-blocking trên function được truyền cho nó.
- take: Tạm dừng cho đến khi nhận được action.
- all: Thực hiện song song tất cả các saga.
