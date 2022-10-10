# useLayoutEffect
- Giống với useEffect chỉ khác thứ tự thực hiện công việc
## useEffect 
- Cập nhật lại state
- Cập nhật lại DOM (mutated)
- Render lại UI 
- Gọi cleanup khi deps thay đổi
- Gọi callback useEffect

## useLayoutEffect
- Cập nhật lại state
- Cập nhật lại DOM (mutated)
- Gọi cleanup khi deps thay đổi (sync)
- Gọi callback useEffect (sync)
- Render lại UI 
