写像型を使用した図書館のVDM++モデルである。

Library1.vppは、仕様実行可能な陽仕様モデルである。
	このモデルは
	　debug new TestRunner().run()
	とすることによりOverture Toolsの回帰テスト・ライブラリを使った回帰テストを実行することができる。
	
	このモデルはCRUDライブラリーを使用し、テスト階層、ビジネスモデル階層、要求辞書階層、ライブラリ階層の4階層からなる。