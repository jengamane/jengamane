import hashlib
import itertools
import string

hashes = [
    "22D8FC89B95AC4A815F86A6C6DB44E18E32BD3684BD67841C943FCCB8334C1C5",
    "7AA95A93646223F48A7E5AA12C4C29FF035670760E0B0998EBD2837187C03137",
    "CFE4734E37E4A3FEACDD0BFCAC51E3AFE8526368785DFCC42E88B85D618AABDC",
    "6FEF50A4EC245A010DD83CB8C78EA24B07C4932AC8D5031981630EA46A793461",
    "24890A97541DA2C621326A833453E081F74F1DF1A24DDBCDD5E49DBDFBFFA24E",
    "EF6536EC01B0095842ED89C9E2102240A832645E5584F78ADF4CCE1B39DA0BA2"
]

def sha256_hash(plate):
    return hashlib.sha256(plate.encode('ascii')).hexdigest().upper()

def find_license_plate(hashes):
    letters = string.ascii_uppercase
    numbers = string.digits

    for letter_combo in itertools.product(letters, repeat=3):
        for number_combo in itertools.product(numbers, repeat=4):
            plate = f"{''.join(letter_combo)}-{''.join(number_combo)}"
            plate_hash = sha256_hash(plate)
            if plate_hash in hashes:
                print(f"Found match: {plate} -> {plate_hash}")
                hashes.remove(plate_hash)
            if not hashes:
                return

find_license_plate(hashes)




