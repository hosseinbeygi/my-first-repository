# qr_generator.py
import qrcode
from datetime import datetime  


def create_qr(data: str, filename: str = None):
    """
    Creates a QR code from the given data and saves it as an image.
    
    :param data: The text or link to encode into a QR code.
    :param filename: Optional custom filename for the QR code image.
    """
    if not filename:
        filename = f"qr_{datetime.now().strftime('%Y%m%d_%H%M%S')}.png"
    
    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_L,
        box_size=10,
        border=4,
    )
    
    qr.add_data(data)
    qr.make(fit=True)

    img = qr.make_image(fill_color="black", back_color="white")
    img.save(filename)

    print(f"✅ QR Code saved as: {filename}")


if __name__ == "__main__":
    text = input("🔗 Enter text or URL to convert into QR code: ")
    create_qr(text)
