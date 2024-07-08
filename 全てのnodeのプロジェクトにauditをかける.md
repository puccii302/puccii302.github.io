# 全てのnodeのプロジェクトにauditをかける

手元にあるnodeのプロジェクト全てに対してauditをかけたい。  
ただし、node以外のプロジェクトもあるので、対象プロジェクトも指定できるようにしたい。

```sh
#!/bin/bash

# 定義するディレクトリのリスト
PROJECT_DIRECTORIES=(
    "/path/to/project1"
    "/path/to/project2"
    "/path/to/project3"
    # 追加のプロジェクトディレクトリをここに追加する
)

# 出力ファイルの名前
OUTPUT_FILE="audit_results.txt"

# 出力ファイルが既に存在する場合は削除
if [ -f "$OUTPUT_FILE" ]; then
    rm "$OUTPUT_FILE"
fi

# 各ディレクトリに対してauditを実行し、結果をテキストファイルに出力
for project in "${PROJECT_DIRECTORIES[@]}"; do
    if [ -d "$project" ]; then
        echo "Running npm audit for $project ..." | tee -a "$OUTPUT_FILE"
        cd "$project"
        npm audit | tee -a "$OUTPUT_FILE"
        echo "Audit results saved to $OUTPUT_FILE"
        cd ..
    else
        echo "Directory $project does not exist." | tee -a "$OUTPUT_FILE"
    fi
    echo "---------------------" | tee -a "$OUTPUT_FILE"  # プロジェクトごとに区切りを挿入
done

echo "Audit process completed."
```