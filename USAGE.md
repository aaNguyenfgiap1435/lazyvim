# Hướng dẫn sử dụng LazyVim

## Bắt đầu

Mở terminal có hỗ trợ màu (không phải terminal `TERM=dumb`), vào thư mục dự án và chạy:

```sh
cd /duong/dan/du-an
nvim                 # mở giao diện chính
nvim ten-file.lua    # mở một tệp
```

Cấu hình ở `/home/linh/work/lazyvim` và được liên kết với `~/.config/nvim`. Neovim cần từ 0.11.2; máy này có 0.12.5. Các phụ thuộc đã có gồm Git, `rg`, `fd`, `fzf`, trình biên dịch C, `curl` và `tree-sitter`. Plugin được tải vào `~/.local/share/nvim`; các công cụ ngôn ngữ được Mason cài theo nhu cầu. [Nerd Font](https://www.nerdfonts.com/) (v3+) không bắt buộc, nhưng nên đặt làm font của terminal để hiển thị biểu tượng đúng. `lazygit` cũng là tùy chọn, chưa được cài sẵn ở đây.

## Thao tác cơ bản

`<leader>` là phím **Space**; ví dụ `<leader>ff` nghĩa là nhấn `Space`, rồi `f`, rồi `f` (không giữ đồng thời). `<C-s>` là Ctrl+S. Bắt đầu ở **Normal mode**; nhấn `i` để vào **Insert mode** (gõ chữ), `Esc` để quay lại Normal mode. Nhấn `Space` và đợi một lát để xem gợi ý phím tắt từ which-key.

| Phím/lệnh | Công dụng |
| --- | --- |
| `h` `j` `k` `l` | Di chuyển trái / xuống / lên / phải |
| `w` / `b`, `0` / `$`, `gg` / `G` | Di chuyển theo từ, đầu / cuối dòng, đầu / cuối tệp |
| `v` / `V` | Chọn ký tự / chọn dòng (Visual mode) |
| `y` / `p`, `dd`, `u`, `Ctrl+r` | Sao chép / dán, xóa dòng, hoàn tác, làm lại |
| `/chuoi` rồi `Enter`; `n` / `N` | Tìm trong tệp; kết quả kế / trước |
| `:w` hoặc `Ctrl+s` | Lưu tệp |
| `:q`, `:wq`, `:q!` | Thoát, lưu rồi thoát, bỏ thay đổi rồi thoát |

## Tệp, bộ đệm và cửa sổ

| Phím | Công dụng |
| --- | --- |
| `Space Space` hoặc `Space ff` | Tìm tệp trong thư mục gốc dự án |
| `Space fF` | Tìm tệp trong thư mục hiện tại |
| `Space /` | Tìm nội dung trong toàn dự án (cần `rg`) |
| `Space e` | Bật/tắt trình duyệt tệp ở gốc dự án |
| `Space E` | Bật/tắt trình duyệt tệp ở thư mục hiện tại |
| `Space ,` | Chọn bộ đệm đang mở |
| `Shift+h` / `Shift+l` | Chuyển bộ đệm trước / sau |
| `Space bd` | Đóng bộ đệm hiện tại |
| `Ctrl+h/j/k/l` | Chuyển giữa các cửa sổ trái / dưới / trên / phải |
| `:split` / `:vsplit` | Chia cửa sổ ngang / dọc |

## Viết mã

| Phím/lệnh | Công dụng |
| --- | --- |
| `gd` | Tới định nghĩa (khi LSP hoạt động) |
| `K` | Xem mô tả ký hiệu (khi LSP hoạt động) |
| `Space ca` | Hành động sửa mã (code actions) |
| `Space cr` | Đổi tên ký hiệu |
| `Space cf` | Định dạng tệp hoặc đoạn đã chọn |
| `Space cd` | Xem chẩn đoán tại dòng hiện tại |
| `]d` / `[d` | Chẩn đoán kế / trước |
| `Space xx` | Danh sách lỗi/chẩn đoán |
| `Space gs` | Xem trạng thái Git |
| `Space ft` | Mở terminal tại gốc dự án |

Một số tính năng như LSP, formatter, lint phụ thuộc vào ngôn ngữ và dự án. Dùng `:Mason` để xem/cài language server hoặc formatter; `:LspInfo` để kiểm tra server đang gắn vào tệp. Dùng `:LazyExtras` để bật các gói ngôn ngữ tùy chọn của LazyVim. Chỉ bật những gói cần dùng; cấu hình mặc định không tự cài server cho mọi ngôn ngữ.

## Quản lý và tùy chỉnh

- `:Lazy` (hoặc `Space l`): xem/cài/cập nhật plugin; `:Lazy sync` để đồng bộ sau khi đổi cấu hình.
- `:LazyHealth`: tải plugin và kiểm tra toàn bộ; `:checkhealth` để kiểm tra Neovim.
- `:Mason`: quản lý công cụ ngôn ngữ.
- `lua/config/options.lua`: thêm tùy chọn; `lua/config/keymaps.lua`: thêm phím tắt; tạo tệp mới trong `lua/plugins/` để thêm/ghi đè plugin. `lua/plugins/example.lua` chỉ là ví dụ **đang tắt**; không bật nguyên tệp đó.
- `lazy-lock.json` lưu phiên bản plugin hiện tại. Nếu cập nhật plugin gây lỗi, kiểm tra thay đổi ở tệp này và dùng giao diện `:Lazy` để khôi phục.

Tài liệu chính thức: [cài đặt](https://www.lazyvim.org/installation), [cấu hình](https://www.lazyvim.org/configuration), [phím tắt đầy đủ](https://www.lazyvim.org/keymaps).

## Xử lý sự cố

- Biểu tượng bị ô vuông: chọn Nerd Font v3+ trong ứng dụng terminal.
- Không tìm được tệp/nội dung: kiểm tra `fd --version` và `rg --version` trong shell; mở Neovim từ đúng thư mục dự án.
- Thiếu gợi ý/LSP: xem `:Mason`, `:LspInfo` và `:LazyHealth`; cài server phù hợp với ngôn ngữ đang dùng.
- Lỗi sau khi sửa cấu hình: xem `:messages`, chạy `:Lazy sync`, rồi mở lại Neovim.
- Nếu muốn hoàn nguyên liên kết cấu hình (chỉ khi không còn muốn dùng thiết lập này): kiểm tra `ls -l ~/.config/nvim` trước, rồi xóa **liên kết**, không xóa thư mục `/home/linh/work/lazyvim`.
