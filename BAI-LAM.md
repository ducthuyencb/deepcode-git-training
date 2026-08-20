# BÀI LÀM — HOMEWORK GITHUB (Git Branch & Workflow)

Tất cả lệnh dưới đây **đã được chạy thật**, không phải lý thuyết.

Thư mục: `~/du an cua thuyen/git-homework/`

| Thư mục | Vai trò |
|---|---|
| `remote/*.git` | 4 bare repo, đóng vai **GitHub** (push/pull/PR-merge/delete đều chạy thật) |
| `git-training/` | Bài 1 → 12 |
| `teammate/` | clone giả lập đồng đội (bài 10 – rebase) |
| `ecommerce/` | Bài 13 |
| `team/devA, devB, devC, lead/` | Bài 14 – 3 developer thật, 3 clone riêng |
| `deepcode-git-training/` | Bài tổng hợp cuối khóa |

## 🔗 Link GitHub (đã đẩy lên thật, public)

| Repo | Link |
|---|---|
| Bài 1–12 | https://github.com/ducthuyencb/git-training |
| Bài 13 | https://github.com/ducthuyencb/ecommerce |
| Bài 14 | https://github.com/ducthuyencb/team-project |
| Bài tổng hợp | https://github.com/ducthuyencb/deepcode-git-training |

**Pull Request thật** (repo `deepcode-git-training`):

| PR | Branch | Trạng thái |
|---|---|---|
| [#1](https://github.com/ducthuyencb/deepcode-git-training/pull/1) | feature/auth | Merged |
| [#2](https://github.com/ducthuyencb/deepcode-git-training/pull/2) | feature/course | Merged |
| [#3](https://github.com/ducthuyencb/deepcode-git-training/pull/3) | feature/payment | Merged |
| [#4](https://github.com/ducthuyencb/deepcode-git-training/pull/4) | feature/report | **Đang mở** (để xem giao diện review) |

---

## Bài 1 — Tạo Repository và Branch
```bash
mkdir git-training && cd git-training
git init
echo "# Git Training" > README.md
git add . && git commit -m "chore: initial project"
git branch -M main
```
✅ Kết quả: `* main`

## Bài 2 — Tạo develop
```bash
git switch -c develop
# thêm mục ## Development vào README.md
git add README.md && git commit -m "docs: add development section"
```
✅ `* develop` / `main`

## Bài 3 — Feature Branch
```bash
git switch -c feature/user-login
# login.txt: Username / Password / Login Button
git add . && git commit -m "feat: add login"
git log --oneline --graph --all
```
✅ Mô hình `main → develop → feature/user-login`

## Bài 4 — Push lên GitHub
```bash
git push -u origin feature/user-login
```
✅ Remote có: `main`, `develop`, `feature/user-login`

## Bài 5 — Merge Feature vào Develop
```bash
git switch develop && git pull origin develop
git merge feature/user-login
git push origin develop
```
✅ Merge fast-forward, develop đã có `login.txt`

## Bài 6 — Feature thứ 2
```bash
git switch develop && git pull
git switch -c feature/user-register
# register.txt
git add . && git commit -m "feat: add user registration"
git push -u origin feature/user-register
```

## Bài 7 — Xóa Branch
```bash
git branch -d feature/user-register          # local
git push origin --delete feature/user-register  # remote
git branch -a
```
✅ `- [deleted] feature/user-register` — branch biến mất cả 2 nơi

## Bài 8 — Merge Conflict 🔥
3 commit sửa **cùng một dòng** ở develop và feature/version → `git merge feature/version`:
```
CONFLICT (content): Merge conflict in README.md
<<<<<<< HEAD
Project version: Develop Version
=======
Project version: Feature Version
>>>>>>> feature/version
```
Xử lý: sửa thành `Project version: Develop Version + Feature Version`, rồi
```bash
git add README.md && git commit -m "fix: resolve version conflict"
```
✅ Log hình chữ Y (merge commit `c8eead1`)

## Bài 9 — Stash
```bash
git stash        # payment.txt biến mất khỏi working dir
git stash list   # stash@{0}: WIP on develop
git stash pop    # lấy lại
```

## Bài 10 — Rebase 🔥
Trong lúc làm `feature/payment`, đồng đội push commit mới lên develop → rebase gây conflict:
```bash
git fetch origin
git rebase develop        # CONFLICT
# sửa file
git add . && git rebase --continue
```
✅ Lịch sử **thẳng hàng**, không có merge commit:
```
feat: add payment
docs: bump develop version   <- commit của đồng đội nằm dưới
```
(Hủy khi cần: `git rebase --abort`)

## Bài 11 — Cherry-pick
```bash
git switch -c feature/test && git commit -m "test: add test file"
git log --oneline          # 15e218d
git switch develop && git cherry-pick 15e218d
```
✅ `test.txt` xuất hiện ở develop

## Bài 12 — Reset và Revert
```bash
git reset --soft HEAD~1   # commit mất, code VẪN staged: "A temp.txt"
git commit -m "feat: add final feature"
git revert HEAD           # tạo commit MỚI: Revert "feat: add final feature"
```
✅ Khác biệt: `reset` xóa lịch sử, `revert` giữ lịch sử và thêm commit hoàn tác (an toàn cho branch chung).

## Bài 13 — Tình huống thực tế (E-Commerce)
3 branch, mỗi branch 2 commit, merge `--no-ff` để giữ vết:
```
feature/login   → feat: create login UI      + feat: implement login validation
feature/product → feat: create product list  + feat: implement product filter
feature/payment → feat: create payment form  + feat: implement payment validation
       ↓ develop ↓ main (release: merge develop into main)
```

## Bài 14 — Git Team Workflow 🔥🔥
3 clone độc lập, 3 tác giả khác nhau (Developer A/B/C) push song song, lead merge:
```
main
|
develop
├── feature/login   (Developer A)
├── feature/product (Developer B)
└── feature/payment (Developer C)
```
✅ develop có đủ 3 file, sau đó `develop → main`.

---

## 🔥🔥🔥 Bài tổng hợp cuối khóa — `deepcode-git-training`

| Yêu cầu | Đã làm |
|---|---|
| ≥3 commit/feature | feature/auth, feature/course, feature/payment đều 3 commit |
| Push lên remote | 9 branch trên remote |
| Pull Request vào develop | **PR thật #1, #2, #3 đã merge trên GitHub**, #4 đang mở |
| ≥1 conflict | README `version:` — develop `1.2.0-develop` vs payment `1.2.0-payment` → resolve thành `1.2.0` |
| ≥1 rebase | `git rebase develop` trên feature/payment + `--continue` |
| ≥1 stash | stash dở dang payment gateway để đi làm `bugfix/login` gấp |
| ≥1 cherry-pick | `feature/logging` → cherry-pick sang develop |

Luồng phát hành đã tạo đủ:
```
feature/* → develop → test → main → production
```

### Xem lại kết quả
```bash
cd ~/"du an cua thuyen"/git-homework/deepcode-git-training && git log --oneline --graph --all
```
