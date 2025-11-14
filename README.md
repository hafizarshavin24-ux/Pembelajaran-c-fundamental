#include <iostream>
#include <string>
#include <vector>
#include <optional>
#include <variant>

class Battery {
public:
    int percentage;
    bool isCharging;

    Battery(int p, bool c) : percentage(p), isCharging(c) {}

    void show() const {
        std::cout << "🔋 Battery: " << percentage << "% "
                  << (isCharging ? "(Charging)" : "(Not Charging)") << "\n";
    }
};

class PerformanceMode {
public:
    enum Mode { POWER_SAVING, BALANCED, HIGH_PERFORMANCE };

    static std::string toString(Mode m) {
        switch (m) {
            case POWER_SAVING: return "Power Saving";
            case BALANCED: return "Balanced";
            case HIGH_PERFORMANCE: return "High Performance";
            default: return "Unknown";
        }
    }
};

class RealmeDevice {
private:
    std::string model;
    Battery battery;
    PerformanceMode::Mode mode;

public:
    RealmeDevice(std::string m, Battery b) 
        : model(std::move(m)), battery(b), mode(PerformanceMode::BALANCED) {}

    void setMode(PerformanceMode::Mode newMode) {
        mode = newMode;
    }

    void showInfo() const {
        std::cout << "\n📱 Realme Device Information\n";
        std::cout << "------------------------------\n";
        std::cout << "Model        : " << model << "\n";
        std::cout << "Mode         : " << PerformanceMode::toString(mode) << "\n";
        battery.show();
        std::cout << "------------------------------\n";
    }
};

int main() {
    RealmeDevice device("Realme GT Neo", Battery(87, false));

    device.showInfo();

    std::cout << "\n⚡ Switching to High Performance Mode...\n";
    device.setMode(PerformanceMode::HIGH_PERFORMANCE);

    device.showInfo();

    return 0;
}
