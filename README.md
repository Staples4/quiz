import java.util.Scanner;

abstract class Pelanggan {
    protected String nama;
    protected double diskon;

    public Pelanggan(String nama) {
        this.nama = nama;
    }

    public String getNama() {
        return nama;
    }

    public abstract double hitungDiskon(double totalBelanja);

    public double hitungNominalDibayar(double totalBelanja) {
        double potongan = totalBelanja * diskon;
        return totalBelanja - potongan;
    }
}

class AnggotaBlasa extends Pelanggan {
    public AnggotaBlasa(String nama) {
        super(nama);
    }

    @Override
    public double hitungDiskon(double totalBelanja) {
        if (totalBelanja >= 1200000) {
            return 0.15; // 15%
        } else if (totalBelanja >= 700000) {
            return 0.1; // 10%
        } else if (totalBelanja >= 300000) {
            return 0.03; // 3%
        } else {
            return 0.0;
        }
    }
}

class NonAnggotaBlasa extends Pelanggan {
    public NonAnggotaBlasa(String nama) {
        super(nama);
    }

    @Override
    public double hitungDiskon(double totalBelanja) {
        return 0.0; // Tidak ada diskon untuk non-anggota Blasa
    }
}

public class DiskonAnggotaBlasa {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Masukkan nama pelanggan: ");
        String namaPelanggan = scanner.nextLine();

        System.out.print("Apakah pelanggan anggota Blasa? (ya/tidak): ");
        String anggotaBlasa = scanner.next();

        System.out.print("Masukkan nominal belanjaan: ");
        int nominalBelanjaan = scanner.nextInt();

        Pelanggan pelanggan;
        if (anggotaBlasa.equalsIgnoreCase("ya")) {
            pelanggan = new AnggotaBlasa(namaPelanggan);
        } else {
            pelanggan = new NonAnggotaBlasa(namaPelanggan);
        }

        double diskon = pelanggan.hitungDiskon(nominalBelanjaan);
        double nominalDibayar = pelanggan.hitungNominalDibayar(nominalBelanjaan);

        System.out.println("\n===== Detail Transaksi =====");
        System.out.println("Nama Pelanggan: " + pelanggan.getNama());
        System.out.println("Jenis Pelanggan: " + (anggotaBlasa.equalsIgnoreCase("ya") ? "Anggota Blasa" : "Bukan Anggota Blasa"));
        System.out.println("Nominal Awal: " + nominalBelanjaan);
        System.out.println("Diskon yang Diperoleh: " + (diskon * 100) + "%");
        System.out.println("Nominal yang Harus Dibayar: " + nominalDibayar);
    }
}
