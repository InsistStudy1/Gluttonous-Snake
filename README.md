# Gluttonous-Snake
C++ 14行代码实现贪吃蛇
```C++
#include <windows.h>
#include <conio.h>
int main() {
	// 30 * 30格子长度
	// -1为食物，> 0为蛇身
	int hX = 0, hY = 0, len = 4, map[900] = { 0 }, c = 'd', c1 = 'd', i = 0;
	// 生成 30 * 30 格子
	srand((unsigned)malloc(!system("mode con:cols=60 lines=30")));
	// 随机生成一个食物，每隔100ms闪屏一次
	for (map[rand() % 900] = -1; 1; Sleep(100)) {
		// 获取输入字符，大小转小写
		if (_kbhit() && (c1 = _getch()) && c1 < 97 ? c1 += 32 : 1)
			// 蛇方向不能对向转动，如：上不能变下
			if (c1 == 'a' && c != 'd' || c1 == 'd' && c != 'a' || c1 == 'w' && c != 's' || c1 == 's' && c != 'w') c = c1;
		// 边界值判断
		if (c == 'a' && --hX < 0 || c == 'd' && ++hX == 30 || c == 'w' && --hY < 0 || c == 's' && ++hY == 30) exit(0);
		// 如果碰到蛇身退出，吃到食物蛇长++
		if (map[hY * 30 + hX] && (map[hY * 30 + hX] > 0 ? exit(0), 1 : ++len))
			//  吃到食物猴随机生成一个食物
			for (i = rand() % 900; map[i] || (map[i] = -1, 0); i = rand() % 900);
		// 每次移动蛇身，移动蛇长度次时，蛇身就会消失
		else for (i = 0; i < 900; i++) map[i] > 0 ? map[i] -=1 : 0;
		// 输出
		for (system("cls"), map[hY * 30 + hX] = len, i = 0; i < 900; i++)
			_cputs(map[i] > 0 ? "()" : map[i] ? "00" : "  ");
	}
}
```
