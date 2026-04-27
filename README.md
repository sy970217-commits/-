'o' 찾기
찾으면 그 위치는 시작점이 됌 시작점 기준으로 오른쪽 방향으로 5칸 범위 내에서 찾기
5개 이상이면 'YES', 아니면 continue
오른쪽 방향 없으면 아래 방향으로 5칸 범위 내에서 찾기
5개 이상이면 'YES', 아니면 continue
아래 방향 없으면 오른쪽 대각선 아래 방향으로 5칸 범위 내에서 찾기
5개 이상이면 'YES', 아니면 continue
오른쪽 대각선 아래 방향 없으면 왼쪽 대각선 방향으로 5칸 범위 내에서 찾기
5개 이상이면 'YES', 아니면 'NO" 출력


import sys
sys.stdin = open('input.txt')

T = int(input())

for tc in range(1, T + 1):
    N = int(input())
    arr = [list(input().strip()) for _ in range(N)]

    # 오른쪽, 아래, 오른쪽 아래, 왼쪽 아래
    dr = [0, 1, 1, 1]
    dc = [1, 0, 1, -1]

    found = False

    for r in range(N):
        if found:
            break
        for c in range(N):
            if arr[r][c] != 'o':
                continue

            # 4방향 검사
            for d in range(4):
                cnt = 1   # 시작점이 이미 'o' 이므로 1부터 시작
                nr, nc = r, c

                # 앞으로 4칸 더 가면서 총 5개 확인
                for _ in range(4):
                    nr += dr[d]
                    nc += dc[d]

                    # 범위 안이고 'o'이면 개수 증가
                    if 0 <= nr < N and 0 <= nc < N and arr[nr][nc] == 'o':
                        cnt += 1
                    else:
                        break

                if cnt >= 5:
                    found = True
                    break

            if found:
                break

    if found:
        print(f"#{tc} YES")
    else:
        print(f"#{tc} NO")
