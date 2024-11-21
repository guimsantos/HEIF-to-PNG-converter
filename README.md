# HEIF-to-PNG Converter  

A simple script to convert **HEIC/HEIF images** to **PNG** using **Google Colab** and **Google Drive**.  

---

## **How It Works**  
1. Place your `.HEIC` files in a folder (e.g., `convert_HEIF_TO_PNG`) in your Google Drive.  
2. Run the script in Google Colab.  
3. The converted `.PNG` files will be saved in another folder (e.g., `converted_HEIF_TO_PNG`).  

---

## **Steps**  

1. **Set Up Google Drive**  
   - Mount Google Drive in your Colab notebook to access the files.  

2. **Prepare Folders**  
   - Input folder: Add `.HEIC` files (e.g., `/convert_HEIF_TO_PNG/`).  
   - Output folder: Specify where converted `.PNG` files will be saved (e.g., `/converted_HEIF_TO_PNG/`).  

3. **Run the Script**  
   - Replace the paths for `input_dir` and `output_dir` with your folder paths.  
   - Execute the script.  

---

## **Requirements**  

Install the necessary libraries in your Colab environment:  
```bash
pip install pillow pyheif
```

---

## **Script**  

```python
from glob import glob
from PIL import Image
import pyheif

input_dir = '/content/drive/MyDrive/convert_HEIF_TO_PNG/*.HEIC'
output_dir = "/content/drive/MyDrive/converted_HEIF_TO_PNG/"
count = 1

for file_path in glob(input_dir):
    heif_file = pyheif.read(file_path)

    image = Image.frombytes(
        heif_file.mode,
        heif_file.size,
        heif_file.data,
        "raw",
        heif_file.mode,
        heif_file.stride,
      )

    image.save(output_dir + str(count) + '.png', 'PNG')

    print(f'Image {count} converted!')
    count += 1
```

---

## **Key Points**  

- **Input Files**: `.HEIC` images in the input folder.  
- **Output Files**: `.PNG` images saved in the output folder.  
- **File Naming**: Converted files are named sequentially (e.g., `1.png`, `2.png`, etc.).  
