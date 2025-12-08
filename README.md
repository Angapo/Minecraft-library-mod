# 📚 Minecraft Library Mod

> ไลบรารี่ที่สร้างขึ้นเพื่อชุมชน - ไม่มีโฆษณา ดาวน์โหลดฟรี 100%

## 🎯 เกี่ยวกับโปรเจค

Mod นี้ถูกสร้างขึ้นด้วยปรัชญาที่ว่า **การเข้าถึงควรเป็นสิทธิของทุกคน** เราเชื่อว่าเครื่องมือและไลบรารี่สำหรับการพัฒนา Minecraft Mod ควรจะเข้าถึงได้ฟรีและง่ายดายสำหรับทุกคน ไม่ว่าคุณจะเป็นนักพัฒนามือใหม่หรือมืออาชีพ

### ✨ ทำไมต้อง Mod นี้?

- **🆓 ฟรี 100%** - ไม่มีค่าใช้จ่ายแอบแฝง ไม่มี premium features
- **🚫 ปลอดโฆษณา** - ไม่มีโฆษณารบกวน ไม่มี adfly หรือลิงก์ย่อที่น่ารำคาญ
- **⚡ ดาวน์โหลดตรง** - ดาวน์โหลดได้ทันทีโดยไม่ต้องรอ
- **🌐 เปิดกว้าง** - สร้างขึ้นเพื่อชุมชน โดยชุมชน
- **🔄 อัพเดตสม่ำเสมอ** - รองรับเวอร์ชันใหม่ล่าสุดของ Minecraft

## 📦 คุณสมบัติ

- ไลบรารี่พื้นฐานสำหรับการพัฒนา Minecraft Mod
- API ที่ใช้งานง่าย เหมาะสำหรับมือใหม่
- เอกสารครบถ้วน เป็นภาษาไทย
- ตัวอย่างโค้ดที่ชัดเจน
- รองรับ Forge และ Fabric

## 🚀 การติดตั้ง

1. ดาวน์โหลด Mod จาก [Releases](../../releases)
2. วาง JAR file ลงในโฟลเดอร์ `mods` ของคุณ
3. เปิด Minecraft และเพลิดเพลิน!

### ความต้องการของระบบ

- Minecraft version: 1.20.x หรือใหม่กว่า
- Forge/Fabric Loader เวอร์ชันล่าสุด
- Java 17 หรือใหม่กว่า

## 💡 การใช้งาน

### การเพิ่ม Dependency

#### สำหรับ Gradle (Forge/Fabric)

```gradle
repositories {
    maven { url 'https://jitpack.io' }
}

dependencies {
    // สำหรับ Forge
    implementation fg.deobf("com.github.yourusername:yourmod:1.0.0")
    
    // สำหรับ Fabric
    modImplementation "com.github.yourusername:yourmod:1.0.0"
}
```

### ตัวอย่างโค้ด

#### 1. การเริ่มต้นใช้งาน

```java
import com.yourlibrary.api.*;

@Mod("yourmod")
public class YourMod {
    public YourMod() {
        // เริ่มต้น Library
        LibraryAPI.initialize();
        
        // ลงทะเบียน Events
        MinecraftForge.EVENT_BUS.register(this);
    }
}
```

#### 2. การสร้าง Custom Block

```java
import com.yourlibrary.api.block.CustomBlock;

public class MyCustomBlock extends CustomBlock {
    public MyCustomBlock() {
        super(Properties.of(Material.STONE)
            .strength(3.0f)
            .requiresCorrectToolForDrops()
        );
    }
    
    @Override
    public void onPlace(BlockState state, Level level, BlockPos pos) {
        // โค้ดของคุณเมื่อวางบล็อก
    }
}
```

#### 3. การสร้าง Custom Item

```java
import com.yourlibrary.api.item.CustomItem;

public class MagicWand extends CustomItem {
    public MagicWand() {
        super(new Properties()
            .stacksTo(1)
            .rarity(Rarity.RARE)
        );
    }
    
    @Override
    public InteractionResultHolder<ItemStack> use(Level level, Player player) {
        // ใช้งานไอเทม
        return InteractionResultHolder.success(player.getItemInHand());
    }
}
```

#### 4. การจัดการ Config

```java
import com.yourlibrary.api.config.Config;

public class ModConfig {
    @Config.Entry(comment = "ความเร็วของผู้เล่น")
    public static double playerSpeed = 1.0;
    
    @Config.Entry(comment = "เปิดใช้งานคุณสมบัติพิเศษ")
    public static boolean enableSpecialFeature = true;
    
    public static void load() {
        Config.load(ModConfig.class, "yourmod-config.json");
    }
}
```

#### 5. การใช้งาน Utility Methods

```java
import com.yourlibrary.api.util.*;

// ตรวจสอบว่าเป็น Server Side หรือ Client Side
if (WorldUtil.isServerSide(level)) {
    // โค้ดสำหรับ Server
}

// หา Block ใกล้เคียง
List<BlockPos> nearbyBlocks = WorldUtil.findNearbyBlocks(
    level, pos, Blocks.DIAMOND_ORE, 10
);

// ส่งข้อความถึงผู้เล่น
PlayerUtil.sendMessage(player, "สวัสดี!");

// เพิ่ม Item ให้ผู้เล่น
ItemUtil.giveItem(player, new ItemStack(Items.DIAMOND, 5));
```

#### 6. การสร้าง Custom Entity

```java
import com.yourlibrary.api.entity.CustomEntity;

public class FriendlyRobot extends CustomEntity {
    public FriendlyRobot(EntityType<?> type, Level level) {
        super(type, level);
    }
    
    @Override
    protected void registerGoals() {
        this.goalSelector.addGoal(1, new FollowOwnerGoal(this));
        this.goalSelector.addGoal(2, new WanderGoal(this));
    }
    
    @Override
    public void tick() {
        super.tick();
        // อัพเดตทุก tick
    }
}
```

#### 7. Event Handling

```java
import com.yourlibrary.api.event.*;

@EventHandler
public class MyEventHandler {
    
    @SubscribeEvent
    public void onPlayerJoin(PlayerJoinEvent event) {
        Player player = event.getPlayer();
        player.sendMessage(Component.literal("ยินดีต้อนรับ!"));
    }
    
    @SubscribeEvent
    public void onBlockBreak(BlockBreakEvent event) {
        if (event.getBlock() == Blocks.DIAMOND_ORE) {
            // ทำอะไรบางอย่างเมื่อขุดเพชร
        }
    }
}
```

## 📖 เอกสาร

### API Reference

**Core Classes:**
- `LibraryAPI` - จุดเริ่มต้นหลักของไลบรารี่
- `CustomBlock` - Base class สำหรับสร้างบล็อกใหม่
- `CustomItem` - Base class สำหรับสร้างไอเทมใหม่
- `CustomEntity` - Base class สำหรับสร้าง Entity ใหม่

**Utility Classes:**
- `WorldUtil` - เครื่องมือจัดการ World และ Dimension
- `PlayerUtil` - เครื่องมือจัดการ Player
- `ItemUtil` - เครื่องมือจัดการ Item
- `BlockUtil` - เครื่องมือจัดการ Block

**Config System:**
- รองรับ JSON และ TOML
- Auto-reload เมื่อมีการแก้ไข
- Type-safe และ comment support

เอกสารฉบับเต็มและตัวอย่างเพิ่มเติมสามารถดูได้ที่ [Wiki](../../wiki) ของโปรเจค

## 🤝 การมีส่วนร่วม

เรายินดีรับการมีส่วนร่วมจากทุกคน! หากคุณต้องการช่วยพัฒนา:

1. Fork โปรเจคนี้
2. สร้าง Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit การเปลี่ยนแปลง (`git commit -m 'Add some AmazingFeature'`)
4. Push ไปยัง Branch (`git push origin feature/AmazingFeature`)
5. เปิด Pull Request

## 📝 License

โปรเจคนี้เผยแพร่ภายใต้ MIT License - ดูรายละเอียดในไฟล์ [LICENSE](LICENSE)

สิ่งนี้หมายความว่า:
- ✅ ใช้งานเชิงพาณิชย์ได้
- ✅ แก้ไขได้
- ✅ แจกจ่ายได้
- ✅ ใช้ส่วนตัวได้

## 💬 ติดต่อและสนับสนุน

- 🐛 พบบั๊ก? รายงานได้ที่ [Issues](../../issues)
- 💭 มีคำถาม? สอบถามได้ที่ [Discussions](../../discussions)
- ⭐ ถูกใจโปรเจคนี้? กด Star ให้กำลังใจเราหน่อย!

## 🙏 ขอบคุณ

ขอบคุณชุมชน Minecraft ไทยทุกคนที่สนับสนุนและให้กำลังใจ

---

**จำไว้เสมอ:** ความรู้และเครื่องมือควรเป็นของทุกคน ไม่ใช่แค่คนที่มีเงิน 🌟

**Made with ❤️ for the Thai Minecraft Community**
