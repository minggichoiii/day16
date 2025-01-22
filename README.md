# day16
import sys
sys.setrecursionlimit(10000)

# 상하좌우 네 방향 탐색 (방향 벡터)
dx = [1, -1, 0, 0]
dy = [0, 0, 1, -1]

# DFS 함수 (재귀로 구현)
def dfs(x, y, field, visited):
    visited[x][y] = True  # 방문 처리
    # 상하좌우 탐색
    for i in range(4):
        nx, ny = x + dx[i], y + dy[i]
        # 배추가 있고, 아직 방문하지 않은 곳으로 이동
        if 0 <= nx < len(field) and 0 <= ny < len(field[0]) and not visited[nx][ny] and field[nx][ny] == 1:
            dfs(nx, ny, field, visited)

def main():
    # 테스트 케이스 개수
    T = int(input())
    
    for _ in range(T):
        # 배추밭 크기(M, N)와 배추의 개수(K)
        M, N, K = map(int, input().split())
        
        # 배추밭 초기화 (0은 배추가 없는 곳, 1은 배추가 있는 곳)
        field = [[0] * N for _ in range(M)]
        
        # 배추가 심어진 위치 처리
        for _ in range(K):
            x, y = map(int, input().split())
            field[x][y] = 1
        
        # 방문 체크 리스트
        visited = [[False] * N for _ in range(M)]
        
        worm_count = 0  # 배추흰지렁이의 수
        
        # 배추밭 탐색
        for i in range(M):
            for j in range(N):
                # 배추가 있고 아직 방문하지 않았다면 DFS를 시작
                if field[i][j] == 1 and not visited[i][j]:
                    # DFS를 실행하여 해당 연결 요소를 모두 방문 처리
                    dfs(i, j, field, visited)
                    worm_count += 1  # 하나의 배추흰지렁이가 필요함
        
        # 배추흰지렁이의 수 출력
        print(worm_count)

if __name__ == "__main__":
    main()
