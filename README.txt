################################################################
#  consistency-reference-prompt
#  使用说明 / USER GUIDE
#  Target file : SKILL.md
#  Version    : 1.0
#  Encoding   : UTF-8 (no BOM)
################################################################

This package is bilingual. PART 1 is Chinese, PART 2 is English.
Both parts use the same section numbers and the same structure.
本文件含中英两版，章节编号与结构完全对应，可对照阅读。


================================================================
PART 1 / 中文版
================================================================

1. 简介
----------------------------------------------------------------
名称      : consistency-reference-prompt
类型      : Agent Skill（SKILL.md = YAML frontmatter + Markdown 指令）
用途      : 从剧本、分镜脚本或人物设定中，为「角色 / 关键道具 / 场景」
            生成一致性参考图（consistency reference image）的生图提示词，
            保证多镜头、多场次之间的人物与物件外观统一。
适用流程  : AI 短剧 / AI 视频 / 分镜预制作 / 角色设定集
重要说明  : 这是一份「提示词生成规范」，不是程序。
            不含代码、不含可执行脚本、不需要安装任何依赖。
            它被 Agent（如 Claude Code、WorkBuddy 等支持 Agent Skills
            规范的工具）读取后，按其中的规则生成英文提示词。

2. 文件清单
----------------------------------------------------------------
F:/skill/
  |- SKILL.md     [必需] skill 本体。文件名固定且大小写敏感，
  |               不可重命名为 skill.md / Skill.md / README.md。
  |- README.txt   [可选] 本说明文件，仅供人阅读，不参与 skill 加载，
                  保留或删除都不影响 skill 功能。

3. 适用场景（对应 SKILL.md 的 "When to Invoke"）
----------------------------------------------------------------
- 需要为短剧 / 分镜中的角色、道具、场景生成一致性参考图提示词
- 需要角色设定表（character sheet）、道具参考图、场景参考图
- 为 AI 视频制作流程批量生成参考图提示词
- 已提供剧本 / 分镜 / 人物小传，希望得到配套的视觉参考提示词

4. 安装方法
----------------------------------------------------------------
4.1 通用规则
    把 SKILL.md 放到「所用工具的 skills 目录 / <skill-name> / SKILL.md」。
    目录名必须与 frontmatter 里的 name 一致，即
    consistency-reference-prompt。

4.2 常见位置（以各工具官方文档为准）
    Claude Code :
      用户级  ~/.claude/skills/consistency-reference-prompt/SKILL.md
      项目级  <project>/.claude/skills/consistency-reference-prompt/SKILL.md
    WorkBuddy :
      用户级  ~/.workbuddy/skills/consistency-reference-prompt/SKILL.md
      项目级  <project>/.workbuddy/skills/consistency-reference-prompt/SKILL.md

4.3 步骤
    1) 新建目录 consistency-reference-prompt
    2) 把 SKILL.md 复制进去
    3) 重启会话 / 刷新工具，让其重新扫描 skills 目录
    4) 用第 5 节的示例指令验证是否触发成功
    无需 npm install、pip install 或任何构建步骤。

5. 使用方法
----------------------------------------------------------------
5.1 触发方式
    直接用自然语言描述需求即可，无需记忆命令。
    建议先把剧本 / 分镜存为 .md 或 .txt 放在工作目录，让 Agent 读取。

5.2 示例指令
    示例 A（完整流程）
      读取分镜脚本 storyboard.md，提取全部角色、关键道具和场景，
      按 SKILL.md 规范生成一致性参考图提示词，保存到
      reference-prompts.md。
    示例 B（单个角色）
      为主角「林夏」生成六视图角色参考表提示词，保持与其他镜头一致。
    示例 C（单个道具）
      为「旧怀表」生成道具参考图提示词，需要同时呈现完整与破损两种状态。
    示例 D（场景）
      为「雨夜的老巷口」生成场景定场镜头提示词，注意暗部保留细节。

5.3 期望输出
    一个新的 Markdown 文件，按「角色 / 道具 / 场景」分组，
    每条提示词是一段可直接复制的英文单段文字（single paragraph），
    可粘贴到 Midjourney / 即梦 / 可灵 / Stable Diffusion 等生图工具。
    每个角色 = 1 条合并提示词（不是 6 条），每个道具 = 1 条，
    每个场景 = 1 条。

6. 输出规范摘要（详见 SKILL.md）
----------------------------------------------------------------
 类别 | 核心规则
 -----+------------------------------------------------------------
 通用 | 无文字 / 无字幕 / 无水印；写实电影质感；电影布光 + 浅景深；
      | 禁止动漫 / 卡通 / 2D 风格；禁止塑料感 AI 皮肤与过度磨皮；
      | 16:9 横构图；轻微手持感、无滤镜感；
      | 角色图与道具图一律纯白背景。
 角色 | 1 条提示词生成 1 张六视图参考表；
      | 左 1/3 纵向排列 3 个头部特写：正面 / 45 度侧面 / 90 度正侧面；
      | 右 2/3 横向排列 3 个全身视图：正面 / 侧面 / 背面；
      | 各区域填满、无画框、无白边、无分隔线；全身为自然站姿、
      | 双臂自然下垂、无动作手势，完整显示手、躯干、腿、脚。
 道具 | 平铺于纯白背景、无阴影、产品摄影式特写；
      | 多状态（开/合、完好/破损）按区域分区，每区完整呈现一种状态；
      | 单状态则同时给出正面与背面；
      | 静态描述、无动作动词、画面中不出现任何人体部位。
 场景 | 广角定场镜头，完整呈现环境、光线、色调、关键陈设与氛围；
      | 夜景 / 弱光场景必须保留暗部细节，禁止死黑。

7. 工作流程（SKILL.md "Workflow" 六步）
----------------------------------------------------------------
    1) 读取剧本 / 分镜，抽取全部角色、关键道具、场景
    2) 为每个角色写外观描述：年龄、体型、发型、面容、肤色、
       服装、配饰、辨识特征、基准表情
    3) 为每个道具写视觉描述：材质、颜色、形状、尺寸、辨识细节
    4) 为每个场景写环境描述：光线、色调、关键家具 / 物件、氛围
    5) 按规范生成提示词，每个角色只产出 1 条合并的六视图提示词
    6) 将全部提示词保存为一个新的 Markdown 文件

8. 安装前检查清单（重要）
----------------------------------------------------------------
  [ ] SKILL.md 文件名与大小写完全正确
  [ ] frontmatter 分隔符是纯 "---"
      标准 Agent Skills 规范必须以纯 --- 开头和结尾；写成 "\---"
      等转义形式会导致部分工具无法解析 frontmatter，
      skill 不会被自动加载。
  [ ] name 值与所在目录名一致（consistency-reference-prompt）
  [ ] description 写清了触发条件，便于 Agent 判断是否调用
  [ ] 文件为 UTF-8 编码，无乱码
  [ ] 输入的剧本 / 素材已获授权，不含隐私或密钥信息
  [ ] 用第 5 节的示例指令实际跑一遍，确认能正常触发并产出文件

9. 常见问题
----------------------------------------------------------------
  Q: 安装后 Agent 识别不到这个 skill？
  A: 优先检查第 8 节：frontmatter 分隔符、目录层级、
     name 与目录名是否一致、是否需要重启会话重新扫描 skills。

  Q: 输入中文剧本可以吗？
  A: 可以。输入语言不限，但按规范输出的提示词统一为英文单段。

  Q: 角色提示词被拆成了 6 条？
  A: 在指令中明确 "one single combined 6-view character sheet prompt"，
     并强调 left one-third / right two-thirds 的分区布局。

  Q: 生成的图里出现了文字或白边？
  A: 规范已含 "No text, no captions, no watermarks"、"no white borders"，
     可在提示词末尾追加负面约束复核。

  Q: 用记事本打开本 txt 中文乱码？
  A: 本文件为 UTF-8（无 BOM），请用支持 UTF-8 的编辑器打开，
     或在 Windows 上用 VS Code / Notepad++ 查看。

如果这个 skill 帮到了你，欢迎为仓库点一个 Star —— 也能让更多人更容易发现它。


================================================================
PART 2 / English Version
================================================================

1. Overview
----------------------------------------------------------------
Name      : consistency-reference-prompt
Type      : Agent Skill (SKILL.md = YAML frontmatter + Markdown rules)
Purpose   : From a script, storyboard, or character bible, generate image
            generation prompts for consistency reference images of
            characters, key props, and scenes, so appearance stays
            identical across shots and episodes.
Use case  : AI short drama / AI video / storyboard pre-production /
            character design bible
Important : This is a prompt-authoring specification, NOT a program.
            No code, no executable script, no dependencies to install.
            An Agent that supports the Agent Skills spec (Claude Code,
            WorkBuddy, etc.) reads it and produces English prompts.

2. File List
----------------------------------------------------------------
F:/skill/
  |- SKILL.md     [Required] The skill itself. Filename is fixed and
  |               case-sensitive; do NOT rename to skill.md,
  |               Skill.md, or README.md.
  |- README.txt   [Optional] This guide, for humans only. Not loaded
                  as a skill. Keeping or removing it is harmless.

3. When to Use (mirrors "When to Invoke" in SKILL.md)
----------------------------------------------------------------
- You need consistency reference image prompts for characters, props,
  or scenes in a drama / storyboard
- You need character sheets, prop references, or scene reference images
- You are producing AI reference images for a drama / video pipeline
- You have a script, storyboard, or character bible and want matching
  visual reference prompts

4. Installation
----------------------------------------------------------------
4.1 General rule
    Place SKILL.md at
    "<your tool's skills dir>/<skill-name>/SKILL.md".
    The directory name MUST match the frontmatter name:
    consistency-reference-prompt.

4.2 Common locations (defer to each tool's official docs)
    Claude Code :
      user   ~/.claude/skills/consistency-reference-prompt/SKILL.md
      proj   <project>/.claude/skills/consistency-reference-prompt/SKILL.md
    WorkBuddy :
      user   ~/.workbuddy/skills/consistency-reference-prompt/SKILL.md
      proj   <project>/.workbuddy/skills/consistency-reference-prompt/SKILL.md

4.3 Steps
    1) Create the directory consistency-reference-prompt
    2) Copy SKILL.md into it
    3) Restart the session / refresh the tool so skills are re-scanned
    4) Verify with an example prompt from section 5
    No npm install, pip install, or build step is needed.

5. Usage
----------------------------------------------------------------
5.1 Triggering
    Just describe the need in natural language; no command to memorize.
    Recommended: save the script / storyboard as .md or .txt in the
    working directory so the Agent can read it.

5.2 Example requests
    Example A (full pipeline)
      Read storyboard.md, extract every character, key prop and scene,
      generate consistency reference prompts per SKILL.md, and save
      them to reference-prompts.md.
    Example B (single character)
      Generate a six-view character reference sheet prompt for the
      lead "Lin Xia", consistent with the other shots.
    Example C (single prop)
      Generate a prop reference prompt for the old pocket watch,
      showing both intact and damaged states.
    Example D (single scene)
      Generate a scene establishing shot prompt for the old alley on a
      rainy night; preserve detail in the shadows.

5.3 Expected output
    A new Markdown file grouped by Character / Prop / Scene. Each prompt
    is one copyable English paragraph, ready to paste into Midjourney,
    Jimeng, Kling, Stable Diffusion, etc.
    One character = ONE combined prompt (not six), one prop = one
    prompt, one scene = one prompt.

6. Output Rules Summary (see SKILL.md for full text)
----------------------------------------------------------------
 Type  | Core rules
 ------+------------------------------------------------------------
 All   | No text / captions / watermarks; realistic cinematic quality;
       | cinematic lighting + shallow depth of field;
       | no anime / cartoon / 2D style; no plastic AI skin or
       | over-smoothing; 16:9 horizontal; slight handheld feel,
       | no filter look; pure white background for character & prop.
 Char  | ONE prompt producing ONE six-view reference sheet;
       | left one-third: 3 head close-ups stacked top-to-bottom —
       | front, 45-degree side, 90-degree profile;
       | right two-thirds: 3 full-body views left-to-right —
       | front, side, back;
       | every section filled completely, no picture frames, no white
       | borders, no divider lines; natural standing pose, arms at
       | sides, no gestures, hands/torso/legs/feet fully visible.
 Prop  | Laid flat on pure white background, no shadows, product-shot
       | close-up; multiple states (open/closed, intact/damaged) split
       | into separate regions, each fully visible in its own zone;
       | single state shows front AND back views;
       | static description, no action verbs, no human body parts.
 Scene | Wide establishing shot covering the full environment,
       | lighting, color palette, key objects and atmosphere;
       | night / low-light scenes must keep shadow detail, no
       | crushed blacks.

7. Workflow (six steps, SKILL.md "Workflow")
----------------------------------------------------------------
    1) Read the storyboard / script; extract all characters, key
       props, and scenes
    2) For each character, describe age, build, hairstyle, face, skin,
       clothing, accessories, distinguishing features, baseline expression
    3) For each prop, describe material, color, shape, size,
       distinguishing details
    4) For each scene, describe lighting, color palette, key furniture /
       objects, atmosphere
    5) Generate prompts per the format — exactly ONE combined six-view
       prompt per character
    6) Save all prompts to a new Markdown file

8. Pre-install Checklist (IMPORTANT)
----------------------------------------------------------------
  [ ] SKILL.md filename and capitalization are exactly correct
  [ ] Frontmatter delimiters are plain "---"
      The Agent Skills spec requires plain --- opening and closing
      lines. An escaped form such as "\---" prevents some tools from
      parsing the frontmatter, and the skill will not be auto-loaded.
  [ ] name matches the directory name (consistency-reference-prompt)
  [ ] description states clear trigger conditions for the Agent
  [ ] File is UTF-8 encoded, with no mojibake
  [ ] Input scripts / assets are properly licensed and contain no
      private data or secrets
  [ ] Run one example from section 5 end-to-end to confirm the skill
      triggers and produces an output file

9. FAQ
----------------------------------------------------------------
  Q: The Agent does not detect the skill after install?
  A: Check section 8 first: frontmatter delimiters, directory depth,
     name vs. directory mismatch, and whether a session restart is
     needed to re-scan skills.

  Q: Can the input script be in Chinese?
  A: Yes. Input language is unrestricted, but the output prompts are
     always single-paragraph English per the spec.

  Q: The character prompt got split into six separate prompts?
  A: State explicitly "one single combined 6-view character sheet
     prompt" and restate the left one-third / right two-thirds layout.

  Q: The generated image contains text or white borders?
  A: The spec already includes "No text, no captions, no watermarks"
     and "no white borders"; re-check or append them as negative
     constraints at the end of the prompt.

  Q: Chinese characters in this .txt look garbled in Notepad?
  A: This file is UTF-8 (no BOM). Open it with a UTF-8-aware editor,
     e.g. VS Code or Notepad++ on Windows.

If this skill has been useful to you, a Star on this repo would be
much appreciated — it also helps others discover it.

################################################################
#  End of document / 文档结束
################################################################
