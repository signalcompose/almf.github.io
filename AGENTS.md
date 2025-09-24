# Agents

This document describes the AI agents and their capabilities in this project.

## Project Overview

**ALMF Official Website** - A music community's official website built with Jekyll and hosted on GitHub Pages.

- **Site URL**: https://almf.info
- **Technology Stack**: Jekyll, GitHub Pages, Minima theme
- **Purpose**: ALMF activity records and music catalog for M3 and other events

## Available Agents

### Web Master Assistant Agent
- **Purpose**: Assists with ALMF website operation, UI/UX improvements, and content management
- **Capabilities**: 
  - Website maintenance and updates
  - UI/UX design and customization
  - Content management and updates
  - Theme customization for music community
  - SEO optimization
  - Performance monitoring
  - GitHub Pages deployment support

### Development Agent
- **Purpose**: Handles code development, debugging, and feature implementation
- **Capabilities**: 
  - Code analysis and refactoring
  - Bug fixing and optimization
  - Feature implementation and custom functionality
  - Code review and suggestions
  - Jekyll plugin development
  - Music-related feature development

### Documentation Agent
- **Purpose**: Manages project documentation and knowledge base
- **Capabilities**:
  - Creating and updating documentation
  - Generating API references
  - Maintaining project guides
  - Content organization and formatting
  - ALMF community documentation
  - Music catalog documentation

### Testing Agent
- **Purpose**: Ensures basic testing and quality assurance
- **Capabilities**:
  - Writing and running essential tests
  - Basic bug validation


### Communication Rules
1. 英語で指示が入力された場合、英文が不自然または誤っているときは正しい英文を提示すること。
2. 修正後の英文を提示した場合は、それを使った指示を再度ユーザーが入力するのを待つこと（英作文練習のため）。
3. 日本語で指示が入力された場合は、その英文訳を提示するだけとし、再入力は促さないこと。
4. AGENTからの返答は指示しない限り日本語で行うこと。
5. 英文の修正はTOEICテストレベル（中級〜上級）の正確性と自然さを基準とすること。

## ALMF-Specific Rules and Guidelines

### Guardrails
1. 破壊的変更は必ず許可を求めること（例: データ削除、URL 構造の変更、レイアウト大幅変更など）
2. 既存機能の互換性を維持すること（既存のページやリンクが壊れないようリダイレクトや対応を行う）
3. 変更は必ずローカルでテストを行い、ビルドエラーがない状態で反映すること
4. **コンテンツの内容は勝手に書き換えない。コンテンツの内容は必ずこちらの指示を仰ぐこと。**
5. **何かコマンド実行する時には必ずPWDして自分のカレントディレクトリを確認すること**
6. 大規模変更は段階的に実施すること（例: デザイン刷新やテーマ変更は一度に全てではなく段階的に）
7. コンテンツやファイル削除時は必ずバックアップを取ること
8. マルチリンガル対応の一貫性を維持すること（日本語と他言語で片方が欠けないようにする）
9. （可能なら）テスト環境または GitHub Pages preview で事前確認を行うこと
10. 機密情報（APIキーや個人情報など）をリポジトリに含めないこと
11. SEO への影響を考慮し、URLやメタデータを変更する際は検索エンジンやリンク切れの影響を確認すること

現状は構築優先のため、main ブランチで作業を行うが、将来的に見直す。

### Content Management
1. **Music Catalog Priority**: Always prioritize music-related content and features
2. **Japanese Language Support**: Ensure proper Japanese language support by using UTF-8 encoding and tools like `jekyll-multiple-languages-plugin` for multilingual content management
3. **M3 Event Integration**: Maintain compatibility with M3 event schedules and releases
4. **Community Focus**: Keep content relevant to ALMF music community activities

### Technical Standards
1. **Jekyll Best Practices**: Follow Jekyll conventions and best practices
2. **GitHub Pages Compatibility**: Ensure all changes work with GitHub Pages deployment
3. **Mobile Responsiveness**: Maintain mobile-friendly design
4. **Performance**: Optimize for fast loading times
5. **SEO**: Implement proper SEO practices for music content discovery

### File Organization
1. **Posts Structure**: Use `_posts/` for news, updates, and announcements
2. **Collections**: Consider using Jekyll collections for music albums/releases
3. **Assets**: Organize images, audio files, and other assets properly
4. **Custom Pages**: Create dedicated pages for different music categories

### Deployment Workflow
1. **Local Testing**: Always test changes locally with `bundle exec jekyll serve`
2. **GitHub Integration**: Use proper Git workflow for GitHub Pages
3. **Custom Domain**: Maintain almf.info domain configuration
4. **Backup**: Ensure content is properly versioned in Git
5. **CI/CD (Optional)**: Implement continuous integration/deployment using tools like GitHub Actions if possible, but not mandatory

### Content Guidelines
1. **Music Metadata**: Include proper metadata for music releases
2. **Event Information**: Keep M3 and other event information up-to-date
3. **Community Updates**: Regular updates on ALMF activities
4. **Accessibility**: Ensure content is accessible to all community members

## Agent Configuration

Each agent can be configured with specific parameters and constraints based on the ALMF project requirements.

## Usage

Agents can be invoked through the project's interface or command-line tools. Each agent has specific commands and options available.

### Common Commands
- `bundle exec jekyll serve` - Local development server
- `bundle exec jekyll build` - Build site for production
- `git push origin main` - Deploy to GitHub Pages

---

*This file was automatically generated and updated for ALMF project. Please update as needed.*