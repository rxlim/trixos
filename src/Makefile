TARGET = kernel
SRCS += main.c
BUILD_DIR = objs


all: $(BUILD_DIR)/$(TARGET)
$(BUILD_DIR):
	mkdir -p $@
$(BUILD_DIR)/%.o: %.c $(BUILD_DIR)
	gcc -c $< -o $@
$(BUILD_DIR)/$(TARGET): $(addprefix $(BUILD_DIR)/,$(SRCS:.c=.o))
	gcc $^ -o $@
clean:
	rm -rf $(BUILD_DIR)
