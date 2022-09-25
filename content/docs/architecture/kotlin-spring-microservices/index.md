---
title: KotlinとSpringを使ったマイクロサービス内のアーキテクチャ設計
date: 2022-09-25T17:59:03
tags:
  - Kotlin
  - Gradle
  - Spring Boot
  - DGS Framework
  - Spring Data JDBC
  - JOOQ
  - PostgreSQL
  - Flyway
  - Kotest
  - Mockk
  - Spring Mockk
description: >
  KotlinとSpringを使ったマイクロサービス内のアーキテクチャ設計について。

draft: true
---

## 作るもの

GraphQLのAPIを持ち，データベースを使用するマイクロサービスを開発します。

## 技術スタック

以下の技術を使用します。

| 技術 | 説明 |
| ---- | ---- |
| Kotlin | プログラミング言語。 |
| Gradle | ビルドツール。 |
| Spring Boot | アプリケーション開発用フレームワーク。 |
| DGS Framework | GraphQLサーバー用フレームワーク。 |
| Spring Data JDBC | ORMフレームワーク。 |
| JOOQ | ORMフレームワーク。 |
| PostgreSQL | データベース。 |
| Flyway | DB Migrationツール。 |
| Kotest | 自動テストフレームワーク。 |
| Mockk/Spring Mockk | モックライブラリ。 |
