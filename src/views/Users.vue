<template>
  <div class="container d-flex justify-content-center pb-5 mt-5">
    
    <!-- การ์ดกระจก -->
    <div class="user-card-3d p-4 p-md-5 w-100">
      
      <!-- หัวข้อ -->
      <h2 class="text-center fw-bold text-gradient title-3d mb-5">
        User List
      </h2>

      <!-- ตารางแสดงข้อมูลผู้ใช้แบบ Floating Rows -->
      <div class="table-responsive">
        <table class="table-glass text-center w-100 align-middle">
          <thead>
            <tr>
              <th>ID</th>
              <th class="text-start">Name</th>
              <th>Email</th>
              <th>City</th>
              <th>Street</th>
            </tr>
          </thead>
          <tbody>
            <!-- ใช้ v-for เพื่อวนลูปแสดงข้อมูลผู้ใช้แต่ละคน -->
            <tr v-for="user in users" :key="user.id" class="row-3d">
              
              <!-- ID -->
              <td>
                <div class="badge-id-3d">
                  {{ user.id }}
                </div>
              </td>
              
              <!-- ชื่อผู้ใช้ -->
              <td class="text-start fw-bold text-dark fs-6">
                {{ user.name }}
              </td>
              
              <!-- อีเมล -->
              <td class="text-primary fw-medium">
                {{ user.email }}
              </td>
              
              <!-- เมือง -->
              <td class="text-secondary-custom fw-bold">
                {{ user.address.city }}
              </td>
              
              <!-- ถนน -->
              <td class="text-muted">
                {{ user.address.street }}
              </td>

            </tr>

            <!-- แสดงข้อความกำลังโหลดเมื่อข้อมูลยังไม่มา -->
            <tr v-if="users.length === 0">
              <td colspan="5" class="text-muted py-5 fs-5">กำลังโหลดข้อมูลผู้ใช้...</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    
    const users = ref([]);

    const fetchUsers = async () => {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/users"
        );
        users.value = await response.json();
      } catch (error) {
        console.error("Error fetching users:", error);
      }
    };

    onMounted(fetchUsers);

    return {
      users, 
    };
  },
};
</script>

<style scoped>

.user-card-3d {
  background: rgba(255, 255, 255, 0.75);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.9);
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.08), 
    inset 0 2px 0 rgba(255, 255, 255, 1);
  max-width: 1100px;
}

.text-gradient {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.title-3d {
  text-shadow: 2px 2px 4px rgba(118, 75, 162, 0.2);
  font-size: 2.5rem;
}
.text-secondary-custom {
  color: #5a6a80;
}

.table-glass {
  border-collapse: separate;
  border-spacing: 0 12px;
}
.table-glass th {
  border: none;
  color: #8c98a4;
  font-weight: 600;
  padding: 10px 15px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.row-3d {
  background: rgba(255, 255, 255, 0.85);
  box-shadow: 0 5px 15px rgba(0,0,0,0.04), inset 0 1px 0 white;
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.3s ease;
}

.row-3d td {
  border: none;
  padding: 18px 15px;
}

.row-3d td:first-child { border-radius: 16px 0 0 16px; }
.row-3d td:last-child { border-radius: 0 16px 16px 0; }

.row-3d:hover {
  transform: translateY(-4px) scale(1.01);
  box-shadow: 0 15px 25px rgba(0,0,0,0.1), inset 0 1px 0 white;
  background: rgba(255, 255, 255, 1);
}

.badge-id-3d {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 45px;
  height: 45px;
  border-radius: 14px;
  background: linear-gradient(135deg, #a18cd1 0%, #fbc2eb 100%);
  color: white;
  font-weight: 800;
  font-size: 1.1rem;
  box-shadow: 
    0 6px 12px rgba(161, 140, 209, 0.4), 
    inset 0 2px 3px rgba(255, 255, 255, 0.5);
  text-shadow: 1px 1px 2px rgba(0,0,0,0.15);
}
</style>