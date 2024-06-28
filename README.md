<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>名前ビンゴ</title>
    <style>
        table {
            width: 100%;
            border-collapse: collapse;
        }
        td {
            width: 20%;
            height: 80px;
            border: 1px solid #000;
            text-align: center;
            vertical-align: middle;
            font-size: 16px;
        }
        .free {
            background-color: #ddd;
        }
    </style>
</head>
<body>
    <h1>名前ビンゴ</h1>
    <table>
        <tbody id="bingo-card">
            <!-- JavaScriptでビンゴカードを生成 -->
        </tbody>
    </table>

    <script>
        function shuffle(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        function createBingoCard() {
            const items = [
                '10代', '20代', '30代', '男性', '女性', '一鉄', '二鉄', '一地下', '二地下',
                '総務', '保全', '道路', '環境', '都市', '福岡出身', '神奈川出身', '埼玉出身',
                '千葉出身', '東京出身', '大阪出身', 'サッカー部', '野球部', 'ワンゲル部', 'バドミントン部', 'ダーツ部'
            ];

            const predefinedItems = [
                '20代', '30代', '男性', '女性',
                '一鉄', '二鉄', '一地下', '二地下'
            ];

            const remainingItems = items.filter(item => !predefinedItems.includes(item));
            const shuffledRemainingItems = shuffle(remainingItems).slice(0, 16); // 16項目に絞る

            const allItems = shuffle([...predefinedItems, ...shuffledRemainingItems]);

            const tbody = document.getElementById('bingo-card');
            let itemIndex = 0;

            for (let i = 0; i < 5; i++) {
                const row = document.createElement('tr');
                for (let j = 0; j < 5; j++) {
                    const cell = document.createElement('td');
                    if (i === 2 && j === 2) {
                        cell.textContent = 'FREE';
                        cell.classList.add('free');
                    } else {
                        cell.textContent = allItems[itemIndex];
                        itemIndex++;
                    }
                    row.appendChild(cell);
                }
                tbody.appendChild(row);
            }
        }

        createBingoCard();
    </script>
</body>
</html>
