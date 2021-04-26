# DoubleBench's JPEG XT

DoubleBench's JPEG XT is a codec for [JPEG XT (ISO/IEC 18477)](https://jpeg.org/jpegxt/ "JPEG XT (ISO/IEC 18477), based on libjpeg.

## 1. Introduction

 [JPEG XT (ISO/IEC 18477)](https://jpeg.org/jpegxt/ "JPEG XT (ISO/IEC 18477)") is an international standard, which specifies a series of backward-compatible extensions to the legacy JPEG standard (ISO/IEC 10918-1).

The JPEG XT image mainly consists of two layers: the base and the extension layer. For backward compatibility to the legacy JPEG standards, the tone-mapped version of the HDR image, called the LDR image, is contained in the base layer. The residual image is generated following one of the proposed profiles by processing a correlation between the original HDR image and a predicted HDR image from the LDR image in the base layer, then coded residual data using the legacy JPEG codec is contained in the extension layer. Codestreams of both are decoded separately and the decoded data is merged to reconstruct the HDR image.

JPEG XT Part 6 and 7 (ISO/IEC 18477-6 and 7) is implemented in DoubleBench's JPEG XT software, which is based on libjpeg and compatible with JPEG XT Reference Software (ISO/IEC 18477-5). Our software supports lossy coding, integer coding, floating-point coding in both encoder and decoder and provides a significant improvement in quality performance when comparing with JPEG XT Reference Software (ISO/IEC 18477-5).

DoubleBench's JPEG XT software also includes a built-in tone mapping operator which generates a better low dynamic range (LDR) base image.

## 2. Open Source Acknowledment

DoubleBench JPEG XT software uses libjpeg library, which is provided inside [libjpeg-turbo](https://libjpeg-turbo.org/ "libjpeg-turbo") for both encoder and decoder.

## 3. Usage
DoubleBench JPEG XT software runs on Windows x64 command prompt.

### 3.1. Encoding
The encoder supports these input's extensions:
- Portable FloatMap (.pfm) for floating-point coding
- Portable Pixmap (.ppm) for integer coding

```sh
jpegxt [optional parameter] input output.jpg
```
List of optional parameter:

| Parameter | Description |
| ------ | ------ |
| -q | Quality parameter for base layer [25..100] |
| -Q | Quality parameter for residual layer [25..100] |
| -r12 | Using 12-bit residual layer. Default is 8 bits. |
| -ldr | Using a 8-bit image (.ppm) as the LDR layer. This option will disable -tmo choice |
| -tmo | Using built in tone mapping operator. 0 is drago03. 1 is reinhard02. |
| -s | Chroma subsampling for base layer. Available value is: 444 and 420. |
| -sr | Chroma subsampling for residual layer. Available value is: 444 and 420. |
| -h | Optimizing JPEG entropy coding. |

### 3.2. Decoding
```sh
jpegxt input.jpg output
```
*(Output extension depend on the encoding process before is floating-point coding or integer coding)*
## 4. Example
```sh
# Encoding
jpegxt -q 75 -Q 75 -r12 -s 420 -sr 444 -h -ldr AtriumNight_drago03.ppm AtriumNight.pfm AltriumNight.jpg
# Decoding
jpegxt AltriumNight.jpg AtriumNight_decoded.pfm
```

## 5. Limitation
- Support only .pfm and .ppm input image for encoding.
- Not support profile A and B.
- Not support lossless coding, alpha channel coding, refinement scans.
- Not support linear transformation for inverse TMO in profile C.

## 6. License
© DoubleBench 2021

## For more details, please visit https://doublebench.com/doublebench-software/#db-software-tabs|1
