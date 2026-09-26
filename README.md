# File-organiser-

import shutil
from pathlib import Path

dir = Path(r"C:\""Documents")

cat = {
    "Images": [".jpg", ".jpeg", ".png", ".gif", ".webp", ".svg"],
    "Videos": [".mp4", ".mkv", ".avi", ".mov"],
    "Documents": [".pdf", ".docx", ".doc", ".txt", ".pptx", ".xlsx"],
    "code": [".py", ".js", ".java", ".cpp", ".c", ".html", ".css"],
    "Archives": [".zip", ".rar", ".7z", ".tar", ".gz"],
    "Audio": [".mp3", ".wav", ".aac"],
}

def organize_files(folder: Path):
    if not folder.exists():
        print("Folder does not exist:", folder)
        return

    for file in folder.iterdir():
        if file.is_file():
            moved = False
            for category, extensions in cat.items():
                if file.suffix.lower() in extensions:
                    target_dir = folder / category
                    target_dir.mkdir(exist_ok=True)
                    shutil.move(str(file), str(target_dir / file.name))
                    moved = True
                    break

            if not moved:
                other_dir = folder / "Other"
                other_dir.mkdir(exist_ok=True)
                shutil.move(str(file), str(other_dir / file.name))

if __name__ == "__main__":
    organize_files(dir)
    print("Files organized successfully!")

