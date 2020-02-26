# basemod添加语法表


 <table>
        <tr>
            <th>语法</th>
            <th>接受参数</th>
            <th>作用</th>
            <th>备注</th>
            <th>所需接口（接口方法可以通过IDE的@override自动寻找）若无需接口可以写在initialize()或构造函数中</th>
        </tr>
        <tr>
            <th>BaseMod.addCard(AbstractCard card)</th>
            <th>card类对象</th>
            <th>向游戏中加入一张卡牌</th>
            <th></th>
            <th> EditCardsSubscribe（void receiveEditCards();）</th>
        </tr>
        <tr>
            <th>BaseMod.addRelicToCustomPool(AbstractRelic relic, AbstractCard.CardColor color)</th>
            <th>遗物类对象relic，卡牌颜色类枚举color</th>
            <th>向游戏中加入自定义颜色遗物</th>
            <th>自定义颜色遗物必须通过该方法添加</th>
            <th> EditRelicsSubscriber（void receiveEditRelics();）</th>
        </tr>
        <tr>
            <th>BaseMod.addRelic(AbstractRelic relic, RelicType type) </th>
            <th>遗物类对象relic，遗物类型枚举type</th>
            <th>向游戏中加入遗物</th>
            <th>type在这里指游戏中已有颜色遗物，包括四色和共享遗物</th>
            <th> EditRelicsSubscriber（void receiveEditRelics();）</th>
        </tr>
            <tr>
            <th>BaseMod.addEvent(String eventID, Class &#60;? extends AbstractEvent &#62; eventClass)</th>
            <th>String类成员遗物ID，事件泛型eventClass</th>
            <th>向游戏中加入自定义事件</th>
            <th>第二个参数可以添加所有继承自 AbstractEvent类的事件子类对象</th>
            <th>   </th>
        </tr>
        </tr>
            <tr>
            <th>BaseMod.addTopPanelItem(TopPanelItem topPanelItem)</th>
            <th>顶部ui对象</th>
            <th>向游戏中加入自定义顶部ui</th>
            <th></th>
            <th>   </th>
        </tr>
        </tr>
            <tr>
            <th>BaseMod.addMonster(String encounterID, String name, GetMonsterGroup group) </th>
            <th>String类对象怪物ID，String类对象怪物名称（可选），怪物对象或怪物组对象</th>
            <th>向游戏中加入自定义怪物</th>
            <th>如果第三个参数传入怪物对象，basemod会调用lambda表达式将怪物自动添加到新怪物组对象（每场战斗怪物以小组单位出现）。</th>
            <th>SetUnlocksSubscriber（receiveSetUnlocks() ）</th>
        </tr>
        </tr>
            <tr>
            <th>BaseMod.addMonsterEncounter(String dungeonID, MonsterInfo encounter)</th>
            <th>String类对象怪物ID，MonsterInfo类对象</th>
            <th>向普通怪物池中加入怪物</th>
            <th>类似的语法还有加入强力怪物池（每一大层的上层）addStrongMonsterEncounter，以及加入精英怪物池addEliteEncounter，传递的参数和功能都是一致的。</th>
            <th>   </th>
        </tr>
        </tr>
            <tr>
            <th>BaseMod.addBoss(String dungeon, String bossID, String mapIcon, String mapIconOutline)</th>
            <th>String类场景（大关卡），String类对象bossID，String类对象地图图标路径，String类对象地图图标轮廓路径</th>
            <th>向游戏中加入新的boss，如果是自定义怪物要先调用addMonster加入该怪物</th>
            <th>这里需要传入两个图片地址，来渲染生成地图上的boss图标。我们根据参数传递可以发现只能将已有的怪物作为boss传递加入，而不能通过该方法同时加入新的怪物作为boss</th>
            <th>   </th>
        </tr>
        </tr>
            <tr>
            <th>puBaseMod.addKeyword(String modID, String proper, String[] names, String description) </th>
            <th>有三个重载方法，至少要传入String类对象数组名称和String对象描述</th>
            <th>加入关键词，一般通过在方法中加载json来获得</th>
            <th>由于杀戮尖塔是多语言的，所以杀戮尖塔的语言文字并不内嵌在代码中，而是加载自json文件，通过config设置语言就可以加载不同的json文件。加载时通过每个对象独有的ID来json文件中搜索对应的名称和描述。关键词则是读取其他描述中出现的对应字符来解释</th>
            <th>EditKeywordsSubscriber（void receiveEditKeywords()）</th>
        </tr>
        </tr>
            <tr>
            <th>BaseMod.addUnlockBundle(CustomUnlockBundle bundle, AbstractPlayer.PlayerClass c, int unlockLevel) </th>
            <th>解锁包类对象bundle，玩家类对象，整形变量解锁等级</th>
            <th>实现升级解锁内容</th>
            <th>一共有五档升级内容，类似于主游戏</th>
            <th>   </th>
        </tr>
        <tr>
            <th>BaseMod.addCharacter(AbstractPlayer character,
									String selectButtonPath,
									String portraitPath,
									PlayerClass characterID,
									String customModeButtonPath)  </th>
            <th>角色类对象，按钮图标路径，背景图路径，角色分类中的ID（比如东方mod人物都为东方类），自定义模式按钮路径（可不写，表示直接使用普通按钮）</th>
            <th>加入新人物</th>
            <th>新人物的构建大部分都是在角色类中构建，这里传入的参数只与开局画面有关</th>
            <th>EditCharactersSubscriber（void receiveEditCharacters() ）</th>
        </tr>
        <tr>
            <th>BaseMod.addColor(AbstractCard.CardColor color, com.badlogic.gdx.graphics.Color bgColor,
								com.badlogic.gdx.graphics.Color backColor, com.badlogic.gdx.graphics.Color frameColor,
								com.badlogic.gdx.graphics.Color frameOutlineColor, com.badlogic.gdx.graphics.Color descBoxColor,
								com.badlogic.gdx.graphics.Color trailVfxColor, com.badlogic.gdx.graphics.Color glowColor,
								String attackBg, String skillBg, String powerBg, String energyOrb,
								String attackBgPortrait, String skillBgPortrait, String powerBgPortrait, String energyOrbPortrait,
								String cardEnergyOrb) </th>
            <th>前面都是颜色类对象，后面分别是攻击卡技能卡能力卡能量玉的小图和大图路径</th>
            <th>加入新的角色颜色</th>
            <th>一般颜色只填一种即可，加入新颜色还需要在官方的枚举类中加入新元素，大图是小图的两倍，格式在正文中有具体展开说明</th>
            <th>   </th>
        </tr>
        <tr>
            <th>BaseMod.addPotion(Class&#60;? extends AbstractPotion&#62; potionClass, Color liquidColor, Color hybridColor, Color spotsColor, String potionID, AbstractPlayer.PlayerClass playerClass) </th>
            <th>药水泛型类对象，药水液体颜色，药水混合颜色，药水高亮颜色，药水ID，玩家种类（不填为通用药水）</th>
            <th>加入新的药水</th>
            <th>药水瓶形状在药水类中定义</th>
            <th>   </th>
        </tr>
        <tr>
            <th>BaseMod.addPower(Class&#60;? extends AbstractPower&#62; powerClass, String powerID) </th>
            <th>力量泛型类对象，力量ID</th>
            <th>加入新的力量</th>
            <th>还没有发现意义，经过测试未经注册的力量也可以直接使用</th>
            <th>   </th>
        </tr>
        <tr>
            <th>BaseMod.addSaveField(String key, CustomSavableRaw saveField) </th>
            <th>保存密钥，要保存的成员</th>
            <th>保存一个成员变量</th>
            <th>还有一种方式是使用basemod的提供的泛型保存接口方法onSave和onLoad</th>
            <th>   </th>
        </tr>
        <tr>
            <th>BaseMod.publishAddAudio(SoundMaster __instance)</th>
            <th>音频对象</th>
            <th>加入一段音频</th>
            <th>杀戮尖塔提供了两个工具类SoundMaster和ImageMaster分别用于处理声音和图像渲染。</th>
            <th></th>
        </tr>
        <tr>
            <th>BaseMod.registerCustomReward(RewardType type, LoadCustomReward onLoad, SaveCustomReward onSave)</th>
            <th>奖励类型对象，加载时调用的函数，保存时调用的函数</th>
            <th>加入新的奖励</th>
            <th>后两个传入的是函数，用于保存和读入你的奖励信息</th>
            <th></th>
        </tr>
        <tr>
            <th>BaseMod.addDynamicVariable(new MyVariable());</th>
            <th>卡牌变量</th>
            <th>加入新的卡牌变量</th>
            <th>可以卡牌描述中加入新的变量，主游戏的变量有伤害值!D! 格挡值!B! 卡牌技能值!M!</th>
            <th></th>
        </tr>
        <tr>
            <th>BaseMod.loadCustomStringsFile(Class class, String filePath)</th>
            <th>描述类，json文件路径</th>
            <th>加载描述文字</th>
            <th>可以使游戏根据ID显示对应的文字</th>
            <th>EditStringsSubscriber(  public void receiveEditStrings() )</th>
        </tr>
   </table>

