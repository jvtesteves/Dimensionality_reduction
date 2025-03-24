# Image Conversion to Grayscale and Binarization

This repository contains a simple project demonstrating how to:

1. **Load** a JPEG image (using the Pillow library).
2. **Convert** the image to grayscale, pixel by pixel, **without** using any built-in conversion methods.
3. **Binarize** the image using a manual threshold.
4. **Display** the three resulting images (original, grayscale, and binarized) side by side, using Matplotlib.

---

## Project Structure

The notebook (or script) is generally composed of the following parts:

1. **Imports and Environment Check**
   - Installs and/or imports the necessary libraries: `Pillow` (for image I/O), `matplotlib` (for displaying images), and `os` (for path checks).
   - Example:
     ```python
     # If Pillow is not installed:
     # !pip install Pillow

     from PIL import Image
     import matplotlib.pyplot as plt
     import os
     ```

2. **Function: `convert_to_grayscale_and_binary(image_path, threshold=128)`**
   - This function reads an image file from the given path (`image_path`).
   - It then **manually** converts each pixel from RGB to a single grayscale value using the approximate NTSC formula:
     ```
     gray_value = 0.299 * R + 0.587 * G + 0.114 * B
     ```
   - Subsequently, it applies a threshold (default = 128) to convert any pixel above or equal to this threshold into white (`255`), and anything below into black (`0`).
   - Returns two Pillow Image objects: one grayscale and one binarized.

3. **Main Execution Steps**
   - Defines the path to the original image (e.g., `/content/lena.jpeg`).
   - Checks if the file exists.
   - Calls the `convert_to_grayscale_and_binary()` function to obtain:
     - A **grayscale** image.
     - A **binarized** image.
   - Saves those images to disk, e.g.:
     ```
     img_gray.save("gray_output.png")
     img_bin.save("binary_output.png")
     ```
   - Uses **Matplotlib** to display the three images side by side: original, grayscale, and binarized.

   Example usage:
   ```python
   image_path = "/content/lena.jpeg"
   img_gray, img_bin = convert_to_grayscale_and_binary(image_path, threshold=128)
   ```

---

## Requirements

- **Python 3.x**
- **Pillow (PIL)**: for image manipulation (loading and saving).
- **Matplotlib**: for displaying images.
- **OS**: only if you need to perform file/path checks (e.g., verifying if the file exists).
- Jupyter Notebook or Google Colab (optional), if you want to run the code interactively.

Installation instructions:
```bash
pip install Pillow matplotlib
```

---

## Usage

1. **Clone or download** this repository (or copy the relevant notebook/script).
2. **Install** the required packages:
   ```bash
   pip install Pillow matplotlib
   ```
3. **Place** your desired image in the same directory or specify the correct path in the code. For example:
   ```python
   image_path = "lena.jpeg"
   ```
4. **Run** the notebook or Python script. You should see:
   - A grayscale version of the original image.
   - A binarized version of the original image (black and white).
   - The three versions displayed side by side in your output or notebook.

---

## Code Explanation

### `convert_to_grayscale_and_binary(image_path, threshold=128)`

- **Input**: 
  - `image_path` (string): path to the input image.
  - `threshold` (int, optional): cutoff value for binarization (default = 128).
- **Process**:
  1. Opens the image with `Image.open(image_path).convert('RGB')`.
  2. Creates two new images: one for grayscale (mode `'L'`) and one for binary (also mode `'L'`).
  3. Iterates through every pixel in the original image, calculates `gray_value`, and then applies the threshold.
  4. Sets each pixel in the respective output images.
- **Returns**:
  - `grayscale_img` (`PIL.Image`): image in 8-bit grayscale.
  - `binarized_img` (`PIL.Image`): image in black and white (0 or 255).

### Displaying Images

- **Matplotlib** usage:
  ```python
  import matplotlib.pyplot as plt

  plt.figure(figsize=(12, 4))

  # Original
  plt.subplot(1, 3, 1)
  plt.imshow(img_original)
  plt.title("Original")
  plt.axis('off')

  # Grayscale
  plt.subplot(1, 3, 2)
  plt.imshow(img_gray, cmap='gray')
  plt.title("Grayscale")
  plt.axis('off')

  # Binarized
  plt.subplot(1, 3, 3)
  plt.imshow(img_bin, cmap='gray')
  plt.title("Binarized")
  plt.axis('off')

  plt.tight_layout()
  plt.show()
  ```

This approach allows a clear side-by-side visualization of the transformations.

---

## Contributing

Feel free to open issues, suggest improvements, or add new examples (e.g., dynamic threshold selection) via pull requests.

---

## License

This project is provided under the [MIT License](https://opensource.org/licenses/MIT). You are free to use, modify, and distribute this code as permitted by the license.
```
