# XueJinBie.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>人生已完成清单-雪尽别</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            background: #f5f5f7;
            font-family: -apple-system, BlinkMacSystemFont, "PingFang SC", "Microsoft YaHei", sans-serif;
            font-size: 10px;
            min-width: 8px;
            line-height: 1.8;
            padding: 12px;
            overflow: hidden;
            height: 100vh;
        }
        /* 角 */
        .header, .tag-group {
            border-radius: 12px;
            -webkit-border-radius: 12px;
            /* 粉 */
            background: #FFF0F5;
            padding: 8px 10px;
            margin-bottom: 8px;
            /* 过 */
            transition: background 2s ease;
        }
        /* 蓝背 */
        .tag-group.full-selected {
            background: #C7E0FF;
        }
        .header {
            text-align: center;
        }
        .title {
            font-size: 14px;
            font-weight: bold;
            /* 渐 */
            background: linear-gradient(90deg, #FF3B30, #007AFF);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 4px;
        }
        .count {
            font-size: 11px;
            font-weight: bold;
            /* 蓝 */
            color: #007AFF;
        }
        .tag-container {
            height: calc(100vh - 70px);
            overflow-y: auto;
            -webkit-overflow-scrolling: touch;
            /* 效果 */
            overscroll-behavior-y: contain;
            scroll-snap-type: y proximity;
        }
        /* 样式 */
        .tag-group {
            display: flex;
            flex-wrap: wrap;
            gap: 4px;
            scroll-snap-align: start;
        }
        /* 标 */
        .tag-group > div:first-child {
            color: #007AFF;
        }
        .tag {
            padding: 3px 6px;
            cursor: pointer;
            transition: transform 0.15s ease, all 0.2s ease;
            white-space: nowrap;
            border-radius: 8px;
            -webkit-border-radius: 8px;
            /* 渐 */
            background: linear-gradient(90deg, #007AFF, #FF3B30);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .tag:hover {
            transform: scale(1.05);
            background-color: #f2f2f7;
        }
        .tag:active {
            transform: scale(0.95);
        }
        /* 选中 */
        .tag.active {
            background: #FF3B30;
            color: #ffffff;
            -webkit-background-clip: unset;
            background-clip: unset;
        }
    </style>
</head>
<body>
    <div class="header">
        <div class="title">人生已完成清单-雪尽别</div>
        <div class="count">已完成: <span id="completedCount">0</span></div>
    </div>
    <div class="tag-container" id="tagContainer">
    <!--二改的傻逼全家都死完了-->
    </div>

    <script>
        // 清单
        const tagGroups = [
            {
                title: "情感上有",
                tags: ["送礼物", "被送礼物", "暗恋", "明恋", "失恋", "表白", "被表白", "放下一个人", "有过遗憾", "爱而不得", "双向奔赴", "当海王", "拒绝他人表白", "表白被拒", "被渣", "犯过傻", "有超过10年的好朋友", "有个无条件可信任的朋友", "买花", "被送花", "给自己买礼物", "向陌生人吐露心声", "拥有要好的异性朋友", "谈恋爱", "被坚定选择", "被背叛", "被伤害", "谈过一场刻骨铭心的恋爱"]
            },
            {
                title: "生活中做过",
                tags: ["留长发", "剪短发", "染发", "漂发", "烫发", "化妆", "做美甲", "装糊涂", "犯校规", "迟到", "旷课", "上课睡觉", "打架被叫家长", "去酒吧", "和朋友去KTV", "断片", "失眠", "睡一天", "吵架", "绝交", "晚上一个人哭", "献血", "住院", "做手术", "晕倒", "会做饭", "做一桌菜", "做饭给家人", "做甜品给喜欢的人", "通宵补作业", "一个人散步", "夜跑", "深夜散心", "一个人出去吃饭", "一个人看电影", "摄影", "一个人去酒吧", "一个人过生日", "一个人逛超市", "一个人去图书馆", "一个人看病", "一个人去唱歌", "社死过", "一个人出门逛", "一个人在外难过", "给自己写信", "出国", "一个人旅游", "跟朋友旅游", "野性消费", "被雪糕刺客伤过", "自己一个人住宾馆", "看鬼片", "去密室", "去鬼屋", "去游乐场", "去看现场演唱会", "去音乐节", "偶遇明星", "去签售会", "在图书馆待一天", "兼职", "打工", "看画展", "捐款", "道歉", "释怀", "失望", "淋雨", "种花", "养宠物", "给父母买衣服", "当伴娘/郎", "摆地摊", "和同学打水仗", "写信", "独自坐飞机", "拼拼图", "办生日会", "健身", "买名牌", "开网店", "练字", "沉迷游戏", "拍毕业照", "放孔明灯", "逛小吃街", "和网友见面", "买唱片", "异地恋", "异国恋", "认识不同国籍的人", "创业", "看极光", "进公司工作", "做未来规划", "搬家", "一个人租房", "转学", "被骗", "撒谎", "改掉一个坏习惯", "在朋友家过夜"]
            },
            {
                title: "学习中的",
                tags: ["考试不及格", "考试第一名", "当班干部", "竞选学生会", "上电视", "上报纸", "登台演出", "主持节目", "演讲", "被老师点名表扬", "被老师点名批评", "全校表扬", "获奖", "学一种外语", "写论文", "写书", "写诗", "写日记", "写剧本", "写歌", "拍影片", "参加比赛", "拍写真", "买相机", "会一种乐器", "有过超过5年的兴趣爱好", "参加志愿活动", "发表成果", "面试成功", "加入校队"]
            },
            {
                title: "体验过",
                tags: ["泡温泉", "跳伞", "坐过山车", "蹦极", "骑马", "卡丁车", "攀岩", "游泳", "滑雪", "滑冰", "旱冰", "滑板", "去野炊", "登山", "看雪", "看海", "看日出", "看日落", "拿驾照", "自驾游", "社团活动", "组建社团", "坐摩天轮"]
            }
        ];

        // 分组
        const container = document.getElementById('tagContainer');
        const countEl = document.getElementById('completedCount');
        let completed = 0;

        tagGroups.forEach(group => {
            const groupEl = document.createElement('div');
            groupEl.className = 'tag-group';
            // 总数
            const totalTags = group.tags.length;
            
            // 标题
            const groupTitle = document.createElement('div');
            groupTitle.style.fontWeight = 'bold';
            groupTitle.style.width = '100%';
            groupTitle.style.marginBottom = '4px';
            groupTitle.textContent = group.title;
            groupEl.appendChild(groupTitle);

            // 内标签
            group.tags.forEach(tagText => {
                const tag = document.createElement('div');
                tag.className = 'tag';
                tag.textContent = tagText;
                
                // 点击
                tag.addEventListener('click', () => {
                    tag.classList.toggle('active');
                    // 更新
                    completed = document.querySelectorAll('.tag.active').length;
                    countEl.textContent = completed;
                    
                    // 检查
                    const activeTagsInGroup = groupEl.querySelectorAll('.tag.active').length;
                    if (activeTagsInGroup === totalTags) {
                        groupEl.classList.add('full-selected');
                    } else {
                        groupEl.classList.remove('full-selected');
                    }
                });
                
                groupEl.appendChild(tag);
            });

            container.appendChild(groupEl);
        });
    </script>
</body>
</html>
